# Jenkins Agents – Types, Usage & Production Best Practices

---

## 1. What is a Jenkins Agent?

A **Jenkins agent** is a machine (or runtime environment) where Jenkins **executes pipeline jobs**.

In simple words:

> Jenkins controller manages pipelines, and **agents do the actual work** like build, test, scan, and deploy.

---

## 2. Why Jenkins Agents are Important

In production, we use agents to:

* Offload heavy builds from the controller
* Improve scalability
* Run parallel jobs
* Isolate workloads
* Reduce risk to Jenkins controller

👉 **Controller should never run builds in production.**

---

## 3. Jenkins Controller vs Agent (Very Important)

| Component  | Responsibility                       |
| ---------- | ------------------------------------ |
| Controller | UI, scheduling, plugins, credentials |
| Agent      | Build, test, scan, deploy            |

---

## 4. Types of Jenkins Agents

---

## 4.1 Static Agents (Permanent Agents)

### What it is

* Fixed machines
* Always connected to Jenkins

### Examples

* VM (EC2)
* Bare metal server

### Pros

* Simple to set up

### Cons

* Not scalable
* Costly
* Manual maintenance

### Production Usage

❌ Rarely used now

---

## 4.2 Dynamic Agents (On-Demand Agents)

### What it is

* Created when job starts
* Destroyed after job finishes

### Pros

* Cost-efficient
* Scalable
* Clean environment every run

### Production Usage

✅ Preferred

---

## 4.3 Docker Agents

### What it is

* Jenkins runs jobs inside Docker containers

### Example Syntax

```groovy
pipeline {
  agent {
    docker {
      image 'maven:3.9-jdk-17'
    }
  }
}
```

### Pros

* Consistent environment
* Fast startup
* Easy dependency management

### Cons

* Requires Docker

### Production Usage

✅ Very common

---

## 4.4 Kubernetes Agents (MOST IMPORTANT)

### What it is

* Jenkins uses Kubernetes to create **ephemeral pod agents**

### How it works

* Each pipeline runs in a new pod
* Pod is destroyed after job completes

### Pros

* Highly scalable
* Cloud-native
* Cost-efficient
* Perfect isolation

### Production Usage

✅✅ **Most used in modern setups**

---

## 4.5 SSH Agents

### What it is

* Jenkins connects to agent via SSH

### Usage

* Legacy setups

### Production Usage

❌ Mostly avoided now

---

## 4.6 Cloud Agents (EC2, Azure VM, GCP)

### What it is

* Agents provisioned dynamically from cloud

### Example

* EC2 plugin

### Production Usage

⚠️ Used, but Kubernetes agents are preferred

---

## 5. Agents We Use Mostly in Production (IMPORTANT)

### Ranking by Real-World Usage

1️⃣ **Kubernetes Agents** – Best practice
2️⃣ **Docker Agents** – Very common
3️⃣ Cloud VM Agents – Limited cases
4️⃣ Static / SSH Agents – Avoided

---

## 6. Why Kubernetes Agents are Preferred

* No long-running build servers
* Automatic scaling
* Works perfectly with:

  * Docker builds
  * Trivy scans
  * SonarQube scans
* Aligns with GitOps & cloud-native architecture

---

## 7. Typical Production Agent Flow

```
Pipeline triggered
   ↓
Jenkins requests agent
   ↓
Kubernetes creates pod
   ↓
Job runs inside pod
   ↓
Pod destroyed
```

---

## 8. Best Practices for Jenkins Agents

* Never run builds on controller
* Use ephemeral agents
* Use Kubernetes or Docker
* Define resource requests/limits
* Keep agents stateless

---

