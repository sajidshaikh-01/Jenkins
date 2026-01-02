# CI & CD – 

## What is CI/CD?

**CI/CD** stands for **Continuous Integration** and **Continuous Delivery / Continuous Deployment**. It is a practice that automates **building, testing, and deploying code** so software can be delivered **faster, safer, and repeatedly**.

---

## 1️⃣ What is Continuous Integration (CI)?

### Simple Definition

Continuous Integration means **developers frequently push code to a shared repository**, and every push is **automatically built and tested**.

### Why CI Exists

Before CI:

* Developers worked on code for days/weeks
* Code conflicts during merge
* Bugs found late

With CI:

* Code is integrated daily
* Bugs are detected early
* Builds are consistent

### CI Workflow (Step-by-Step)

1. Developer writes code
2. Pushes code to Git repository
3. CI tool is triggered automatically
4. Code is built
5. Automated tests run
6. Result is reported (pass/fail)

### What Happens if CI Fails?

* Build stops
* Team is notified
* Code is **not allowed to move forward**

### Example CI Tasks

* Compile code (Java, Go, Node)
* Run unit tests
* Run linting / static code analysis
* Build Docker image

---

## 2️⃣ What is Continuous Delivery (CD)?

### Simple Definition

Continuous Delivery means **code is always in a deployable state**, and deployment happens **with manual approval**.

### Key Point

✅ Deployment is ready
❌ Deployment is **not automatic**

### CD Workflow

1. CI pipeline succeeds
2. Artifacts are stored (Docker image, JAR, etc.)
3. Code is deployed to staging
4. Manual approval is required
5. Deployed to production

### Where Continuous Delivery is Used

* Banking applications
* Enterprise systems
* Critical production environments

---

## 3️⃣ What is Continuous Deployment?

### Simple Definition

Continuous Deployment means **every successful change is automatically deployed to production** without human approval.

### Key Point

✅ Fully automated
✅ Fast releases
❌ Higher risk if tests are poor

### Continuous Deployment Workflow

1. Code pushed to Git
2. CI pipeline runs
3. Tests pass
4. Automatically deployed to production

### Where Continuous Deployment is Used

* Startups
* SaaS products
* Feature-driven platforms

---

## 4️⃣ CI vs Continuous Delivery vs Continuous Deployment

| Feature          | CI  | Continuous Delivery | Continuous Deployment |
| ---------------- | --- | ------------------- | --------------------- |
| Code Integration | Yes | Yes                 | Yes                   |
| Automated Tests  | Yes | Yes                 | Yes                   |
| Manual Approval  | No  | Yes                 | No                    |
| Auto Prod Deploy | No  | No                  | Yes                   |

---

## 5️⃣ How CI/CD Works in Real Production (End-to-End)

### Real-Life Flow

```
Developer → Git Push
        → CI (Build + Test)
        → Artifact Created
        → CD (Deploy to Staging)
        → Approval (optional)
        → Production Deployment
```

### Tools Commonly Used

* Git (source control)
* CI tool (Jenkins, GitHub Actions, GitLab CI)
* Docker (build images)
* Artifact Registry (ECR, Docker Hub)
* Kubernetes / VM (deployment)

---

## 6️⃣ Why CI/CD is Important in Production

### Business Benefits

* Faster releases
* Fewer bugs
* Faster feedback
* Reliable deployments

### Engineering Benefits

* Automated testing
* No manual errors
* Consistent environments
* Easy rollback

---

## 7️⃣ Common Interview Questions & Answers

**Q: What problem does CI solve?**
A: It prevents integration issues by testing every code change early.

**Q: Difference between Continuous Delivery and Continuous Deployment?**
A: Delivery requires manual approval; Deployment is fully automatic.

**Q: Can CD exist without CI?**
A: No. CI is the foundation of CD.

---

## 8️⃣ Production Best Practices

* Always fail fast in CI
* Run tests before deployment
* Use separate environments (dev, staging, prod)
* Never deploy untested code
* Secure secrets using vaults or CI credentials

---

