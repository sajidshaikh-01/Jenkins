# Jenkinsfile – Syntax, Explanation & Pipeline Types 
## What is a Jenkinsfile?

A **Jenkinsfile** is a **text file** that defines the entire CI/CD pipeline **as code**.

* Written in **Groovy-based syntax**
* Stored in the **same Git repository as the application code**
* Read by Jenkins to execute the pipeline

📌 Think of Jenkinsfile as:

> "A step-by-step instruction file that tells Jenkins how to build, test, and deploy code."

---

## Why Jenkinsfile is Important in Production

Before Jenkinsfile:

* Pipelines configured in UI
* No version control
* Hard to audit or rollback

With Jenkinsfile:

* Pipeline is version controlled
* Changes reviewed via PR
* Same pipeline for all environments
* Easy rollback

👉 **Every modern Jenkins setup uses Jenkinsfile**

---

## Where Jenkinsfile Lives

```
application-repo/
 ├── src/
 ├── Dockerfile
 ├── Jenkinsfile   👈
 └── README.md
```

Jenkins automatically reads the Jenkinsfile from the repo.

---

## Types of Jenkins Pipelines

Jenkins supports **two pipeline styles**:

1️⃣ Declarative Pipeline (Recommended)
2️⃣ Scripted Pipeline (Advanced / Legacy)

---

# 1️⃣ Declarative Pipeline (MOST USED 🔥)

## What is Declarative Pipeline?

Declarative pipeline uses a **structured, opinionated syntax** that is easy to read and maintain.

* Simple
* Less error-prone
* Preferred in production

---

## Basic Declarative Jenkinsfile (Example)

```groovy
pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Building the application'
      }
    }

    stage('Test') {
      steps {
        echo 'Running tests'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploying application'
      }
    }
  }
}
```

---

## Declarative Pipeline Syntax Explained

### `pipeline {}`

* Root block
* Mandatory

---

### `agent`

Defines **where the pipeline runs**.

Examples:

* `agent any` → Run on any available agent
* `agent none` → Define agent per stage

---

### `stages {}`

Container for all pipeline stages.

---

### `stage('name')`

Logical step in pipeline (Build, Test, Deploy).

---

### `steps {}`

Commands executed inside a stage.

---

## Common Declarative Blocks (Production)

### `environment`

Used to define environment variables.

```groovy
environment {
  APP_ENV = 'prod'
}
```

---

### `post`

Used for actions after pipeline execution.

```groovy
post {
  success {
    echo 'Pipeline successful'
  }
  failure {
    echo 'Pipeline failed'
  }
}
```

---

### `when`

Used for conditional execution.

```groovy
when {
  branch 'main'
}
```

---

### `tools`

Defines tools required (JDK, Maven).

---

## Why Declarative is Preferred in Production

* Clean syntax
* Built-in error handling
* Easier to secure
* Easier for teams

---

# 2️⃣ Scripted Pipeline (ADVANCED)

## What is Scripted Pipeline?

Scripted pipeline is written in **pure Groovy**.

* Very flexible
* Very powerful
* Harder to read

---

## Basic Scripted Pipeline Example

```groovy
node {
  stage('Build') {
    echo 'Building'
  }

  stage('Test') {
    echo 'Testing'
  }

  stage('Deploy') {
    echo 'Deploying'
  }
}
```

---

## Scripted Pipeline Explained

### `node {}`

* Allocates an agent

### `stage {}`

* Defines pipeline stages

Scripted pipelines rely on Groovy logic like:

* loops
* if/else
* functions

---

## Declarative vs Scripted Pipeline (IMPORTANT)

| Feature        | Declarative | Scripted   |
| -------------- | ----------- | ---------- |
| Syntax         | Structured  | Free-form  |
| Ease of use    | Easy        | Hard       |
| Error handling | Built-in    | Manual     |
| Production use | ✅ Yes       | ⚠️ Limited |
| Recommended    | ✅ Yes       | ❌ No       |

---

## Which One Should YOU Use?

👉 **Declarative Pipeline** for:

* All new projects
* Production pipelines
* Interviews

👉 Scripted Pipeline only when:

* You need very complex logic
* Maintaining legacy pipelines

---

## Real Production Jenkinsfile Flow

```
Checkout Code
 → Build
 → Test
 → Security Scan
 → Docker Build
 → Push Image
 → Deploy
```



