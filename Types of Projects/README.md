# Jenkins Project Types Used in REAL Production (Only)
---
## ✅ 1️⃣ Pipeline Project (MOST IMPORTANT 🔥)

### What it is

A **Pipeline project** defines the complete CI/CD workflow as **code** using a `Jenkinsfile`.

### Why it is used in production

* Pipeline stored in Git (version controlled)
* Easy to review and audit
* Reproducible builds
* Supports complex CI/CD logic

### Typical Production Use

* Build application
* Run tests
* Build Docker image
* Push to registry
* Deploy to Kubernetes / VM

### Interview Line

> Almost all modern Jenkins setups use Pipeline projects because they support pipeline-as-code.

---

## ✅ 2️⃣ Multibranch Pipeline Project (PRODUCTION STANDARD 🔥🔥)

### What it is

A **Multibranch Pipeline** automatically creates pipelines for **each branch** in a Git repository.

### Why it is used in production

* Automatically detects branches
* Separate pipeline per branch
* Supports PR validation
* Works perfectly with Git workflows

### Typical Production Use

* Feature branch CI
* Pull Request validation
* Main / release branch deployments

### Interview Line

> Multibranch pipelines are the industry standard for Git-based CI/CD.

---

## ✅ 3️⃣ Organization Folder (Large-Scale Production)

### What it is

Automatically scans a **GitHub/GitLab organization** and creates Multibranch pipelines for all repositories.

### Why it is used in production

* Handles hundreds of repositories
* Zero manual job creation
* Scales well for microservices

### Typical Production Use

* Enterprises
* Platform teams
* Microservice-based architectures

---

## ✅ 4️⃣ Folder Project (Supporting Role)

### What it is

Used only to **organize Jenkins jobs** in the UI.

### Why it is used in production

* Environment-wise grouping (dev / stage / prod)
* Team-wise organization

⚠️ Note: Not a CI/CD engine, only for structure

---

## ❌ Jenkins Project Types NOT Used in Modern Production

You can safely **ignore these for interviews**:

* Freestyle Project (legacy)
* Matrix Project (rare)
* External Job (almost never used)

---

## 🎯 What YOU Should Focus On (Very Important)

### Must Know (100%)

* Pipeline Project
* Multibranch Pipeline

### Good to Know (Bonus)

* Organization Folder
* Folder Project

---

## Real Production Mapping

| Scenario               | Jenkins Project Type |
| ---------------------- | -------------------- |
| Single repo CI/CD      | Pipeline             |
| Feature branches & PRs | Multibranch Pipeline |
| Many microservices     | Organization Folder  |
| Job organization       | Folder               |

---

