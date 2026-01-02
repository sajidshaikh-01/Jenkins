# Jenkins Pipeline Parameters 

---

## What are Pipeline Parameters?

**Pipeline parameters** allow you to **pass input values to a Jenkins pipeline at runtime**.

In simple words:

> Parameters let you control pipeline behavior **without changing the Jenkinsfile**.

---

## Why Parameters are Used (Very Important)

Parameters are used to:

* Deploy to different environments (dev / stage / prod)
* Choose branches
* Enable or disable steps
* Control versions or tags

👉 Without parameters, you must edit the Jenkinsfile every time.

---

## Where Parameters are Defined

Parameters are defined **inside the Jenkinsfile** using the `parameters {}` block.

They appear as **input fields** when you click **Build with Parameters**.

---

## Basic Parameter Syntax

```groovy
pipeline {
  agent any

  parameters {
    string(name: 'ENV', defaultValue: 'dev', description: 'Deployment environment')
  }

  stages {
    stage('Print Value') {
      steps {
        echo "Environment is: ${params.ENV}"
      }
    }
  }
}
```

---

## How Parameters Are Used in Pipeline

* Jenkins shows input fields before build
* User selects or enters values
* Values are accessed using `params.<PARAM_NAME>`

Example:

```groovy
${params.ENV}
```

---

## Important Parameter Types (ONLY USED IN PRODUCTION)

### 1️⃣ String Parameter

Used for:

* Environment name
* Version
* Tag

```groovy
string(name: 'VERSION', defaultValue: 'v1.0.0', description: 'App version')
```

---

### 2️⃣ Choice Parameter (MOST USED 🔥)

Used for:

* Environment selection

```groovy
choice(name: 'ENV', choices: ['dev', 'stage', 'prod'], description: 'Select environment')
```

---

### 3️⃣ Boolean Parameter

Used for:

* Enable / disable steps

```groovy
booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests or not')
```

---

## Practical Production Example (Simple & Real)

```groovy
pipeline {
  agent any

  parameters {
    choice(name: 'ENV', choices: ['dev', 'stage', 'prod'], description: 'Environment')
    booleanParam(name: 'RUN_TESTS', defaultValue: true, description: 'Run tests')
  }

  stages {
    stage('Test') {
      when {
        expression { params.RUN_TESTS }
      }
      steps {
        echo 'Running tests'
      }
    }

    stage('Deploy') {
      steps {
        echo "Deploying to ${params.ENV}"
      }
    }
  }
}
```

---

## Key Rules (Remember These)

* Parameters are evaluated **before pipeline starts**
* Parameters are **read-only** during execution
* Parameters avoid Jenkinsfile changes
* `params` object is used to access values

---
