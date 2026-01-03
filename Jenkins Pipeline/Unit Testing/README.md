# Unit Testing – What, Why & How We Use It in Production
---

## What is Unit Testing?

**Unit testing** is the practice of testing the **smallest testable parts of an application (units)** in isolation.

A **unit** usually means:

* A function
* A method
* A class

Simple definition:

> Unit testing checks whether a small piece of code works correctly on its own.

---

## Why Unit Testing is Important

In production-grade software:

* Code changes happen frequently
* Many developers work on the same codebase

Unit testing helps to:

* Catch bugs early
* Prevent breaking existing functionality
* Give confidence during deployments

👉 The earlier a bug is found, the cheaper it is to fix.

---

## What Unit Testing is NOT

* It does NOT test the full application flow
* It does NOT test databases or external APIs directly
* It does NOT replace integration or end-to-end testing

---

## How Unit Testing is Used in Production

### Typical Production Flow

1. Developer writes code
2. Developer writes unit tests
3. Code is pushed to Git
4. CI pipeline runs unit tests
5. If tests fail → pipeline stops
6. If tests pass → pipeline continues

Unit tests act as a **quality gate**.

---

## Where Unit Testing Runs in CI/CD

Unit tests usually run:

* After code checkout
* Before build artifacts are deployed

Typical order:

```
Checkout → Unit Tests → Build → Scan → Deploy
```

---

## Components of Unit Testing (VERY IMPORTANT)

### 1️⃣ Test Framework

Used to write and run unit tests.

Examples:

* Java: JUnit, TestNG
* Python: pytest, unittest
* JavaScript: Jest, Mocha
* Go: testing

---

### 2️⃣ Test Runner

* Executes test cases
* Reports pass/fail results

Often built into the test framework.

---

### 3️⃣ Assertions

Assertions check expected vs actual output.

Example (conceptual):

* Expected result = 10
* Actual result = function output

If they don’t match → test fails.

---

### 4️⃣ Mocks / Stubs

Used to replace:

* Databases
* External APIs
* Third-party services

Why?

* Unit tests must be isolated
* External dependencies make tests slow and unreliable

---

### 5️⃣ Test Data

* Input values for tests
* Covers normal cases and edge cases

---

## Example: Unit Testing in a Jenkins Pipeline

```groovy
pipeline {
  agent any

  stages {
    stage('Unit Tests') {
      steps {
        sh 'mvn test'
      }
    }
  }
}
```

What happens:

* Jenkins runs unit tests
* If tests fail → pipeline fails
* Code never reaches production

---

## Production Best Practices

* Write unit tests for core logic
* Run unit tests on every commit or PR
* Keep tests fast
* Mock external dependencies
* Do not skip unit tests to save time

---
