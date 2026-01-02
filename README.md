# Jenkins Architecture – 

## What is Jenkins Architecture?

Jenkins architecture defines **how Jenkins components interact** to execute CI/CD pipelines efficiently, securely, and at scale. In production, Jenkins follows a **Controller–Agent (Master–Worker)** model.

---

## High-Level Jenkins Architecture Diagram

```
                 ┌──────────────────────────┐
                 │        Developers         │
                 │   (Git Push / PR / Tag)   │
                 └─────────────┬────────────┘
                               │
                               ▼
                   ┌─────────────────────┐
                   │   Source Control     │
                   │   (GitHub / GitLab)  │
                   └─────────────┬────────┘
                                 │ Webhook
                                 ▼
        ┌────────────────────────────────────────┐
        │        Jenkins Controller (Master)      │
        │-----------------------------------------│
        │ - Web UI                                │
        │ - Job Configuration                     │
        │ - Pipeline Orchestration                │
        │ - Plugin Management                     │
        │ - Credentials Management                │
        │ - Scheduling Builds                     │
        └───────────────┬────────────────────────┘
                        │ Assign Job
                        ▼
        ┌────────────────────────────────────────┐
        │           Jenkins Agents                │
        │-----------------------------------------│
        │ - Run Build Steps                       │
        │ - Execute Tests                         │
        │ - Build Docker Images                   │
        │ - Deploy Applications                   │
        │ - Temporary or Permanent                │
        └───────────────┬────────────────────────┘
                        │
                        ▼
          ┌─────────────────────────────────┐
          │ Deployment Targets               │
          │ (VMs / Kubernetes / Cloud)       │
          └─────────────────────────────────┘
```

---

## Core Jenkins Components (Explained One by One)

---

## 1️⃣ Jenkins Controller (Master)

### What is Jenkins Controller?

The **Controller** is the brain of Jenkins. It **does not execute builds** in production. Instead, it **manages and coordinates everything**.

### Responsibilities

* Hosts Jenkins Web UI
* Stores job configurations
* Manages pipelines and stages
* Schedules builds
* Manages plugins
* Stores credentials
* Communicates with agents

### Production Best Practice

❌ Do NOT run builds on controller
✅ Use controller only for orchestration

---

## 2️⃣ Jenkins Agents (Workers / Nodes)

### What are Jenkins Agents?

Agents are machines or environments where **actual build, test, and deployment steps run**.

### Agent Types

* Static agents (VM-based)
* Docker-based agents
* Kubernetes dynamic agents (most common today)

### Responsibilities

* Execute pipeline steps
* Compile code
* Run tests
* Build Docker images
* Deploy applications

### Production Rule

> Agents should be **ephemeral and stateless** whenever possible.

---

## 3️⃣ Executor

### What is an Executor?

An **executor** is a **slot** on an agent that runs one job at a time.

### Example

* 1 agent with 2 executors → 2 jobs can run in parallel

### Production Recommendation

* Limit executors per agent
* Avoid resource exhaustion

---

## 4️⃣ Jenkins Jobs

### What is a Job?

A job defines **what Jenkins should do**.

### Job Types

* Freestyle (legacy)
* Pipeline (recommended)
* Multibranch Pipeline (production standard)

### Production Usage

✅ Pipelines stored as code (`Jenkinsfile`)

---

## 5️⃣ Jenkins Pipeline

### What is a Pipeline?

A pipeline is a **series of automated steps** written as code to build, test, and deploy applications.

### Pipeline Stages

* Build
* Test
* Scan
* Package
* Deploy

### Why Pipelines?

* Version controlled
* Reproducible
* Reviewable

---

## 6️⃣ Jenkins Plugins

### What are Plugins?

Plugins extend Jenkins functionality.

### Common Plugins

* Git
* Pipeline
* Docker
* Kubernetes
* Slack
* Credentials

### Production Warning

❌ Too many plugins = instability
✅ Install only what you need

---
