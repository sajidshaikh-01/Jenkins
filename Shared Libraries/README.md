# Jenkins Shared Libraries – Explained Clearly (with Syntax & Example)

---

## 1. What are Jenkins Shared Libraries?

Jenkins Shared Libraries are **reusable Groovy code** that allow you to **share common pipeline logic** across multiple Jenkins pipelines.

In simple words:

> Instead of writing the same Jenkinsfile logic again and again, we write it once in a shared library and reuse it.

---

## 2. Why Shared Libraries are Used (Production Reason)

In real production environments, we use shared libraries to:

* Avoid duplicate Jenkinsfile code
* Standardize CI/CD pipelines across teams
* Make pipelines clean and readable
* Apply security and best practices centrally
* Update logic in one place for all pipelines

### Interview One-Liner

> "Jenkins shared libraries help us centralize and reuse pipeline logic, making CI/CD pipelines consistent and maintainable."

---

## 3. Where Shared Libraries are Stored

Shared libraries are stored in a **separate Git repository**.

Example repo name:

```
jenkins-shared-library
```

---

## 4. Shared Library Directory Structure (VERY IMPORTANT)

```
jenkins-shared-library/
├── vars/
│   └── buildApp.groovy
├── src/
│   └── org/example/utils.groovy
└── resources/
    └── templates.yaml
```

### What Each Folder Means

* `vars/` → Global pipeline functions (most commonly used)
* `src/` → Helper classes (advanced use)
* `resources/` → Static files (YAML, JSON, scripts)

---

## 5. Simple Shared Library Example (Most Common)

### Step 1: Create a Function in `vars/`

File:

```
vars/buildApp.groovy
```

```groovy
def call() {
    echo "Building application..."
    sh 'mvn clean package'
}
```

👉 The `call()` method makes this function callable directly.

---

## 6. Configure Shared Library in Jenkins

Jenkins UI:

```
Manage Jenkins → Configure System → Global Pipeline Libraries
```

Add:

* Name: `my-shared-lib`
* Default version: `main`
* Source: Git repository URL

---

## 7. Use Shared Library in Jenkinsfile (Syntax)

### Import Library

```groovy
@Library('my-shared-lib') _
```

### Use Function

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                buildApp()
            }
        }
    }
}
```

---

## 8. Parameterized Shared Library Example

### Shared Library Function

```groovy
def call(String env) {
    echo "Deploying to ${env} environment"
    sh "kubectl apply -f deployment-${env}.yaml"
}
```

### Jenkinsfile Usage

```groovy
deployApp('prod')
```

---

## 9. Real Production Use Cases

Shared libraries are commonly used for:

* Docker image build logic
* SonarQube scanning
* Trivy vulnerability scanning
* Helm deployments
* Slack / email notifications

Example:

```groovy
sonarScan()
trivyScan()
buildDockerImage()
```

---

## 10. Shared Libraries vs Normal Jenkinsfile

| Jenkinsfile       | Shared Library    |
| ----------------- | ----------------- |
| Pipeline-specific | Reusable          |
| Duplicate logic   | Centralized logic |
| Hard to maintain  | Easy to update    |
| Long files        | Clean pipelines   |

---

## 11. Best Practices (Production)

* Keep Jenkinsfiles thin
* Move logic to shared libraries
* Version shared libraries (branch/tag)
* Test shared libraries before prod
* Avoid business logic in Jenkinsfile

---
