# Dependency Scanning – How It Works & How We Use It in Production

---

## What is Dependency Scanning?

**Dependency scanning** checks your application’s **third-party libraries** (dependencies) for **known security vulnerabilities**.

In simple words:

> Your code may be safe, but the libraries you use might not be.

---

## Why Dependency Scanning Is Important

Modern applications use:

* Open-source libraries
* Frameworks
* Language package managers (npm, pip, Maven, etc.)

If a dependency has a vulnerability:

* Your application becomes vulnerable
* Even without writing insecure code

👉 Most real attacks happen through **vulnerable dependencies**.

---

## How Dependency Scanning Works (Step by Step)

1. Scanner reads dependency files

   * `package.json`
   * `requirements.txt`
   * `pom.xml`
   * `go.mod`

2. Scanner builds a dependency list

3. Dependencies are matched against vulnerability databases

   * CVE (Common Vulnerabilities and Exposures)
   * NVD

4. Scanner reports:

   * Vulnerability ID (CVE)
   * Severity (Low / Medium / High / Critical)
   * Affected versions

5. Pipeline decides:

   * Warn only OR
   * Fail build (for high/critical issues)

---

## What Dependency Scanning Does NOT Do

* It does NOT scan your source code logic
* It does NOT fix issues automatically (usually)
* It does NOT replace code scanning (SAST)

---

## Tools Used for Dependency Scanning in Production

Below are **tools that are actually used in real companies**.

---

## 1️⃣ OWASP Dependency-Check (Very Common)

### What it is

* Open-source dependency vulnerability scanner

### How it works

* Scans dependency manifests
* Matches dependencies with CVE database

### Why used in production

* Free
* Easy to integrate
* Language agnostic

### Limitation

* Can be slow
* Needs CVE database updates

---

## 2️⃣ Snyk (MOST USED IN CLOUD-NATIVE 🔥)

### What it is

* Commercial security scanning tool

### How it works

* Scans dependencies
* Uses its own vulnerability database
* Provides fix suggestions

### Why used in production

* Accurate results
* Developer-friendly
* Good CI/CD integration

### Used by

* Startups
* SaaS companies

---

## 3️⃣ GitHub Dependabot

### What it is

* Built-in GitHub dependency scanner

### How it works

* Scans dependencies in repo
* Opens PRs with fixes

### Why used in production

* Zero setup
* Tight GitHub integration

### Limitation

* GitHub-only
* Less customizable

---

## 4️⃣ Trivy (VERY POPULAR 🔥)

### What it is

* Open-source security scanner

### What it scans

* Dependencies
* Container images
* OS packages

### Why used in production

* Fast
* Simple CLI
* Works well with Docker & Kubernetes

---

## Which Tools Are MOST COMMON in Production

| Company Type              | Tool                   |
| ------------------------- | ---------------------- |
| Enterprises               | OWASP Dependency-Check |
| Cloud-native / SaaS       | Snyk                   |
| GitHub-first teams        | Dependabot             |
| Kubernetes / Docker heavy | Trivy                  |

---

## Where Dependency Scanning Runs in CI/CD

Usually runs:

* After code checkout
* Before Docker build OR
* Before deployment

Typical order:

```
Build → Dependency Scan → Image Build → Deploy
```

---

## Jenkins Pipeline Example (Simple & Real)

### Example: Dependency Scanning with Trivy

```groovy
pipeline {
  agent any

  stages {
    stage('Install Trivy') {
      steps {
        sh 'curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh'
      }
    }

    stage('Dependency Scan') {
      steps {
        sh 'trivy fs --severity HIGH,CRITICAL --exit-code 1 .'
      }
    }
  }
}
```

---

## What This Pipeline Does

* Scans project dependencies
* Fails pipeline if HIGH or CRITICAL issues found
* Stops vulnerable code from reaching production

---
