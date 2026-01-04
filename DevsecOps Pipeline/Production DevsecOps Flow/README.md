# End-to-End Jenkinsfile (Production CI – DevSecOps Ready)

> This Jenkinsfile represents a **real production CI pipeline** used in modern DevSecOps setups.
> It covers **build → test → SAST → image scan → push → GitOps trigger**.

---

## 🔹 Production CI Flow Covered

* Source checkout
* Dependency install
* Unit testing + code coverage
* SonarQube SAST + Quality Gate
* Docker image build
* Trivy vulnerability scanning
* Push image to Docker registry
* Update GitOps repo (CD trigger)

---

## 🔹 Assumptions (Important)

* Jenkins runs on Kubernetes
* Builds run on **ephemeral Kubernetes agents**
* SonarQube and Docker credentials are already configured in Jenkins
* Trivy is available in the agent image

---

## 🔹 Jenkinsfile (Complete & Realistic)

```groovy
@Library('my-shared-lib') _

pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: ci
    image: docker:24.0
    command:
    - cat
    tty: true
    volumeMounts:
    - name: docker-sock
      mountPath: /var/run/docker.sock
  volumes:
  - name: docker-sock
    hostPath:
      path: /var/run/docker.sock
"""
    }
  }

  environment {
    IMAGE_NAME = "sajidshaikh/myapp"
    IMAGE_TAG  = "${BUILD_NUMBER}"
    SONARQUBE_ENV = "sonarqube"
  }

  stages {

    stage('Checkout Code') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Unit Tests + Coverage') {
      steps {
        sh 'npm test -- --coverage'
      }
    }

    stage('SAST - SonarQube Scan') {
      steps {
        withSonarQubeEnv(SONARQUBE_ENV) {
          sh '''
            sonar-scanner \
            -Dsonar.projectKey=myapp \
            -Dsonar.sources=. \
            -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info
          '''
        }
      }
    }

    stage('Quality Gate') {
      steps {
        timeout(time: 2, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }

    stage('Build Docker Image') {
      steps {
        sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
      }
    }

    stage('Trivy Image Scan') {
      steps {
        sh "trivy image --severity HIGH,CRITICAL --exit-code 1 ${IMAGE_NAME}:${IMAGE_TAG}"
      }
    }

    stage('Push Image to Registry') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh '''
            echo $PASS | docker login -u $USER --password-stdin
            docker push ${IMAGE_NAME}:${IMAGE_TAG}
          '''
        }
      }
    }

    stage('Update GitOps Repo') {
      steps {
        sh '''
          git clone https://github.com/your-org/gitops-repo.git
          cd gitops-repo
          sed -i "s|image: .*|image: ${IMAGE_NAME}:${IMAGE_TAG}|" deployment.yaml
          git add deployment.yaml
          git commit -m "Update image to ${IMAGE_TAG}"
          git push origin main
        '''
      }
    }
  }

  post {
    failure {
      echo '❌ Pipeline failed. Deployment blocked.'
    }
    success {
      echo '✅ CI successful. GitOps CD will deploy automatically.'
    }
  }
}
```

---

## 🔹 Why This Jenkinsfile is Production-Grade

* No builds on controller
* Ephemeral Kubernetes agents
* Security gates before image push
* SonarQube blocks bad code
* Trivy blocks vulnerable images
* GitOps used for CD (no kubectl in Jenkins)

---

