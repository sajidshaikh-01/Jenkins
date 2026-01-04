# Jenkins Interview Questions & Answers (50+) + Mock Interview

---

## 🔹 Section 1: Jenkins Basics (Q1–Q10)

**Q1. What is Jenkins?**
Jenkins is an open-source CI/CD automation server used to build, test, scan, and deploy applications.

**Q2. Why do we use Jenkins?**
To automate software delivery, reduce manual errors, and enable fast feedback.

**Q3. Is Jenkins CI or CD?**
Both. Jenkins handles CI and can orchestrate CD, but modern CD is often done using GitOps tools.

**Q4. What language is Jenkins written in?**
Java.

**Q5. What is a Jenkins job?**
A job defines a task Jenkins executes, such as build or test.

**Q6. What are Jenkins pipelines?**
Pipelines define CI/CD as code using a Jenkinsfile.

**Q7. What is Jenkinsfile?**
A text file that defines pipeline logic and is stored in Git.

**Q8. Declarative vs Scripted pipeline?**
Declarative is structured and preferred in production; Scripted is flexible but complex.

**Q9. Can Jenkins run on Docker?**
Yes, Jenkins itself and its agents can run in Docker.

**Q10. What are Jenkins plugins?**
Extensions that add functionality like Git, Docker, SonarQube.

---

## 🔹 Section 2: Architecture & Agents (Q11–Q20)

**Q11. What is Jenkins controller?**
The main node that manages jobs, UI, plugins, and scheduling.

**Q12. What is a Jenkins agent?**
A machine or environment where pipelines actually run.

**Q13. Should we run builds on controller?**
No, builds should run on agents in production.

**Q14. Types of Jenkins agents?**
Static, Docker, Kubernetes, Cloud-based, SSH.

**Q15. Which agents are most used in production?**
Kubernetes-based ephemeral agents.

**Q16. Why Kubernetes agents are preferred?**
They are scalable, isolated, cost-efficient, and cloud-native.

**Q17. What is an ephemeral agent?**
An agent created for a job and destroyed after completion.

**Q18. How Jenkins scales?**
By adding agents and running jobs in parallel.

**Q19. Where is Jenkins workspace located?**
Inside agent filesystem, usually under `/var/lib/jenkins/workspace`.

**Q20. What happens if agent goes down?**
The job fails or is rescheduled depending on configuration.

---

## 🔹 Section 3: CI/CD, DevSecOps (Q21–Q35)

**Q21. How Jenkins integrates with Git?**
Using webhooks and Git plugins.

**Q22. What is code coverage?**
It measures how much code is executed during tests.

**Q23. Does Jenkins calculate code coverage?**
No, test tools generate coverage; Jenkins orchestrates.

**Q24. What is SAST?**
Static code analysis to find vulnerabilities without executing code.

**Q25. Is SonarQube SAST?**
Yes.

**Q26. What are Quality Gates?**
Rules that decide pass/fail of code quality and security.

**Q27. How Jenkins uses SonarQube?**
Runs scanner and blocks pipeline based on quality gate.

**Q28. What is Trivy?**
A vulnerability scanner for container images and dependencies.

**Q29. When do we run Trivy in pipeline?**
After image build and before pushing to registry.

**Q30. What happens if Trivy finds CRITICAL CVEs?**
Pipeline fails.

**Q31. Jenkins vs GitHub Actions?**
Jenkins is self-hosted and flexible; GitHub Actions is SaaS.

**Q32. Jenkins role in GitOps?**
Jenkins handles CI; GitOps tools handle CD.

**Q33. Should Jenkins deploy directly to Kubernetes?**
No, it should update GitOps repo instead.

**Q34. What is Pipeline as Code?**
Managing CI/CD logic via version-controlled files.

**Q35. How do you secure Jenkins?**
RBAC, credentials store, minimal plugins, HTTPS.

---

## 🔹 Section 4: Advanced & Production (Q36–Q50)

**Q36. What are Jenkins shared libraries?**
Reusable pipeline code stored in Git.

**Q37. Why shared libraries are important?**
They reduce duplication and standardize pipelines.

**Q38. How Jenkins handles secrets?**
Using credentials store and secret bindings.

**Q39. What is CSRF protection in Jenkins?**
Protects against fake POST requests using crumbs.

**Q40. How to handle high load in Jenkins?**
Use agents, limit plugins, scale horizontally.

**Q41. How Jenkins supports parallel execution?**
Using parallel stages.

**Q42. Can Jenkins run jobs in parallel?**
Yes.

**Q43. Jenkins freestyle vs pipeline job?**
Pipeline is code-based and preferred.

**Q44. How Jenkins handles failures?**
Stage-level failure handling and post actions.

**Q45. How Jenkins integrates with Docker?**
Via Docker plugin or Docker agents.

**Q46. What is Blue Ocean?**
A visual UI for Jenkins pipelines.

**Q47. Is Blue Ocean used in production?**
Rarely; mainly for visualization.

**Q48. How do you upgrade Jenkins safely?**
Backup, test plugins, upgrade controller first.

**Q49. Jenkins HA setup?**
HA via external storage and load balancer.

**Q50. Biggest Jenkins mistake beginners make?**
Running builds on controller.

---

## 🔹 Section 5: Mock Interview (Real Interviewer Style)

**Interviewer:** Explain your Jenkins setup.
**You:** We use Jenkins for CI with Kubernetes-based ephemeral agents. Jenkins builds, tests, performs SAST and image scanning, and updates a GitOps repo for deployment.

**Interviewer:** How do you ensure security in Jenkins pipelines?
**You:** By integrating SonarQube for SAST, Trivy for image scanning, enforcing quality gates, and blocking pipelines on critical issues.

**Interviewer:** Who deploys to Kubernetes? Jenkins or Argo CD?
**You:** Jenkins never deploys directly. It updates Git, and Argo CD handles deployment.

**Interviewer:** Where does Jenkins run in your setup?
**You:** Jenkins runs on Kubernetes, and all builds run on dynamic pod agents.

**Interviewer:** What happens if SonarQube quality gate fails?
**You:** The Jenkins pipeline stops and the image is not promoted.

**Interviewer:** Why Kubernetes agents instead of static VMs?
**You:** Better scalability, isolation, and cost efficiency.

---
