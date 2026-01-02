# Jenkins Project Types – 
---

## What is a Jenkins Project?

A **Jenkins project (job)** defines **what Jenkins should do** when it is triggered.
Examples:

* Build code
* Run tests
* Build Docker images
* Deploy applications

---

## 1️⃣ Freestyle Project (Legacy)

### What is it?

Freestyle is the **oldest and simplest** Jenkins job type. Everything is configured through the **UI**.

### Characteristics

* UI-based configuration
* Step-by-step commands
* No code versioning

### Example Use Case

* Simple shell script execution
* Quick testing jobs

### Why NOT used in production?

❌ Not version controlled
❌ Hard to review changes
❌ Not scalable

### Interview Tip

> Freestyle jobs are mostly legacy and rarely used in modern production.

---

## 2️⃣ Pipeline Project (MOST IMPORTANT 🔥)

### What is it?

A Pipeline project defines CI/CD **as code** using a `Jenkinsfile`.

### Characteristics

* Written in Groovy
* Stored in Git
* Fully version controlled
* Reproducible

### Example Use Case

* Build → Test → Docker → Deploy

### Why used in production?

✅ Pipeline as Code
✅ Easy rollback
✅ Reviewable

### Interview Tip

> Almost all modern Jenkins setups use Pipeline projects.

---

## 3️⃣ Multibranch Pipeline Project (🔥🔥 PRODUCTION STANDARD)

### What is it?

A Multibranch Pipeline automatically creates pipelines for **each branch** in a Git repository.

### Characteristics

* Automatically detects branches
* Separate pipeline per branch
* Uses `Jenkinsfile` in repo

### Example Use Case

* CI for feature branches
* PR validation

### Why used in production?

✅ Best for Git-based workflows
✅ Automatic branch handling
✅ Scales well

### Interview Tip

> Multibranch pipelines are the standard for enterprise CI/CD.

---

## 4️⃣ Folder Project

### What is it?

Folders are used to **organize jobs** in Jenkins UI.

### Example Use Case

* Team-wise pipelines
* Environment-wise pipelines

### Production Usage

✅ Used for organization

---

## 5️⃣ Organization Folder

### What is it?

Automatically scans a **GitHub / GitLab organization** and creates Multibranch pipelines for all repositories.

### Example Use Case

* Large enterprises
* Multiple microservices

### Production Usage

✅ Very common in large companies

---

## 6️⃣ External Job

### What is it?

Used to **track jobs executed outside Jenkins**.

### Production Usage

❌ Rarely used

---

## 7️⃣ Matrix Project (Advanced / Rare)

### What is it?

Runs the same job across **multiple combinations** (OS, JDK, versions).

### Example Use Case

* Library testing
* Cross-platform builds

### Production Usage

⚠️ Limited use

---

## 8️⃣ GitHub Organization Project

### What is it?

Similar to Organization Folder but specific to GitHub.

### Production Usage

✅ Used when GitHub is primary SCM

---

## Which Jenkins Project Types Should YOU Focus On?

### For Learning & Interviews

1️⃣ Pipeline Project
2️⃣ Multibranch Pipeline
3️⃣ Folder / Organization Folder

### You can IGNORE (for now)

* Freestyle
* Matrix
* External jobs

---

## Real Production Mapping

| Scenario          | Project Type         |
| ----------------- | -------------------- |
| Simple CI/CD      | Pipeline             |
| Feature branches  | Multibranch Pipeline |
| Microservices org | Organization Folder  |
| Legacy systems    | Freestyle            |

---

## Interview-Ready Summary (MEMORIZE)

> Jenkins provides multiple project types, but modern production primarily uses Pipeline and Multibranch Pipeline projects because they support pipeline-as-code, scalability, and Git-based workflows.

---

