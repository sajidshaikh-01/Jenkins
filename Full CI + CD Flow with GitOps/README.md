# Full CI + CD Flow with GitOps (Production Architecture)

---

## 1. What is CI + CD with GitOps?

In modern production systems:

* **CI (Continuous Integration)** = Build, test, scan, package
* **CD (Continuous Deployment)** = Deploy automatically using **Git as the source of truth**
* **GitOps** = Deployment is driven by Git, not by CI tools

> CI builds artifacts. GitOps CD deploys artifacts.

---

## 2. High-Level Architecture Overview

```
Developer
   │
   ▼
Application Git Repo (Source Code)
   │
   │  Commit / Pull Request
   ▼
CI Pipeline (Jenkins / GitHub Actions)
   │
   ├─ Build
   ├─ Install Dependencies
   ├─ Unit Tests + Code Coverage
   ├─ SAST (SonarQube + Quality Gate)
   ├─ Build Docker Image
   ├─ Image Scan (Trivy)
   ├─ Push Image to Registry
   │
   ▼
GitOps Repo (Manifests / Helm / Kustomize)
   │  Image tag update
   ▼
GitOps CD Tool (Argo CD / Flux)
   │  Sync
   ▼
Kubernetes Cluster (EKS)
```

---

## 3. CI Flow (Continuous Integration) – Explained Step by Step

### 3.1 Code Commit

* Developer pushes code to **application repository**
* Pull Request triggers CI pipeline

Purpose:

* Fast feedback
* Early failure detection

---

### 3.2 Build Stage

* Application is compiled or packaged
* Ensures code is syntactically correct

Failure here = broken code

---

### 3.3 Dependency Installation

* Application dependencies are installed
* Examples:

  * `npm install`
  * `pip install`
  * `mvn install`

Risk addressed:

* Vulnerable libraries

---

### 3.4 Unit Testing + Code Coverage

* Unit tests validate business logic
* Coverage report generated

Output:

* Coverage report file

Why:

* Prevent untested code
* Measure test effectiveness

---

### 3.5 SAST – Static Code Analysis

Tool:

* SonarQube

What happens:

* Source code scanned (no execution)
* Coverage imported
* Bugs, vulnerabilities, code smells detected

Quality Gate:

* Minimum coverage
* No critical vulnerabilities

❌ If gate fails → CI stops

---

### 3.6 Docker Image Build

* Application packaged into a container image
* Immutable artifact created

Why:

* Same image across all environments

---

### 3.7 Image Vulnerability Scanning

Tool:

* Trivy

What happens:

* Scans OS and app dependencies
* Checks CVEs

Policy:

* Fail on HIGH / CRITICAL

❌ If vulnerabilities found → CI stops

---

### 3.8 Push Image to Registry

* Only **approved images** are pushed
* Registry examples:

  * Docker Hub
  * AWS ECR

Image tag becomes deployment reference

---

## 4. CD Flow with GitOps – Explained Step by Step

---

### 4.1 Separate GitOps Repository

Contains:

* Kubernetes manifests
* Helm charts or Kustomize

Important rule:

> CI never deploys directly to Kubernetes

---

### 4.2 Image Tag Update (Git Commit)

* CI updates image tag in GitOps repo
* Change is committed and pushed

This commit = deployment request

---

### 4.3 GitOps CD Tool Watches Repo

Tool examples:

* Argo CD
* Flux

What happens:

* Tool continuously monitors GitOps repo
* Detects desired vs actual state

---

### 4.4 Sync & Reconciliation

* GitOps tool pulls latest manifests
* Applies changes to Kubernetes
* Reconciles drift automatically

Git = single source of truth

---

### 4.5 Kubernetes Deployment

* Pods updated using rolling update
* Health checks applied
* Rollback possible by Git revert

---

## 5. Why Companies Use CI + CD with GitOps

* Clear separation of responsibilities
* Strong audit trail
* Easy rollback
* No manual kubectl access
* Secure & scalable

---

## 6. CI vs CD Responsibility Split (Very Important)

| Area     | Tool            | Responsibility             |
| -------- | --------------- | -------------------------- |
| CI       | Jenkins         | Build, test, scan, package |
| Artifact | Docker Registry | Store images               |
| CD       | Argo CD         | Deploy & reconcile         |
| Control  | Git             | Source of truth            |

---

## 7. Interview-Ready Explanation (Say This)

> "In our setup, CI handles building, testing, and security scanning. Once the image is approved, CI updates the GitOps repository. Argo CD continuously watches that repo and deploys the changes to Kubernetes, ensuring Git remains the single source of truth."

---
