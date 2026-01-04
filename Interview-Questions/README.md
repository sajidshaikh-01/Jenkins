# Jenkins Interview Questions & Answers (50+) + Mock Interview

---

## 🔹 Section 1: Jenkins Basics (Q1–Q10)

**Q1. What is Jenkins?**
Jenkins is an open-source CI/CD automation server used to build, test, scan, and deploy applications.

---

**Q2. Why do we use Jenkins?**
We use Jenkins to automate software delivery, reduce manual errors, and get fast feedback on every code change.

---

**Q3. Is Jenkins CI or CD?**
Jenkins supports both CI and CD. In modern setups, Jenkins mainly handles CI, while CD is done using GitOps tools.

---

**Q4. What language is Jenkins written in?**
Jenkins is written in Java.

---

**Q5. What is a Jenkins job?**
A Jenkins job is a task or process that Jenkins executes, such as building, testing, or deploying code.

---

**Q6. What are Jenkins pipelines?**
Jenkins pipelines define CI/CD workflows as code using a Jenkinsfile.

---

**Q7. What is a Jenkinsfile?**
A Jenkinsfile is a text file stored in Git that defines the entire CI/CD pipeline.

---

**Q8. Declarative vs Scripted pipeline?**
Declarative pipelines are structured and preferred in production, while Scripted pipelines are flexible but complex.

---

**Q9. Can Jenkins run on Docker?**
Yes, Jenkins and its agents can both run inside Docker containers.

---

**Q10. What are Jenkins plugins?**
Jenkins plugins extend Jenkins functionality, such as Git, Docker, and SonarQube integration.

---

## 🔹 Section 2: Architecture & Agents (Q11–Q20)

**Q11. What is Jenkins controller?**
The Jenkins controller manages the UI, job scheduling, plugins, and credentials.

---

**Q12. What is a Jenkins agent?**
A Jenkins agent is a machine or environment where pipeline jobs are executed.

---

**Q13. Should we run builds on the controller?**
No. In production, builds should always run on agents, not on the controller.

---

**Q14. What are the types of Jenkins agents?**
Static agents, Docker agents, Kubernetes agents, cloud-based agents, and SSH agents.

---

**Q15. Which Jenkins agents are mostly used in production?**
Kubernetes-based ephemeral agents are most commonly used.

---

**Q16. Why are Kubernetes agents preferred?**
They provide scalability, isolation, cost efficiency, and are cloud-native.

---

**Q17. What is an ephemeral agent?**
An ephemeral agent is created for a job and destroyed after the job finishes.

---

**Q18. How does Jenkins scale?**
Jenkins scales by adding more agents and running jobs in parallel.

---

**Q19. Where is the Jenkins workspace located?**
The workspace is located on the agent filesystem, usually under `/var/lib/jenkins/workspace`.

---

**Q20. What happens if an agent goes down?**
The running job fails or is rescheduled depending on configuration.

---

## 🔹 Section 3: CI/CD & DevSecOps (Q21–Q35)

**Q21. How does Jenkins integrate with Git?**
Jenkins integrates with Git using webhooks and Git plugins.

---

**Q22. What is code coverage?**
Code coverage measures how much of the source code is executed during tests.

---

**Q23. Does Jenkins calculate code coverage?**
No. Coverage tools generate reports, and Jenkins only orchestrates the process.

---

**Q24. What is SAST?**
Static Application Security Testing scans source code for vulnerabilities without executing it.

---

**Q25. Is SonarQube a SAST tool?**
Yes, SonarQube performs static code analysis and security checks.

---

**Q26. What are Quality Gates?**
Quality Gates are rules that decide whether code passes or fails quality and security standards.

---

**Q27. How does Jenkins use SonarQube?**
Jenkins runs the SonarQube scanner and blocks the pipeline if the quality gate fails.

---

**Q28. What is Trivy?**
Trivy is a vulnerability scanner for container images and application dependencies.

---

**Q29. When do we run Trivy in a pipeline?**
After building the Docker image and before pushing it to the registry.

---

**Q30. What happens if Trivy finds CRITICAL vulnerabilities?**
The pipeline fails and the image is not promoted.

---

**Q31. Jenkins vs GitHub Actions?**
Jenkins is self-hosted and highly flexible, while GitHub Actions is a managed SaaS solution.

---

**Q32. What is Jenkins’ role in GitOps?**
Jenkins handles CI, while GitOps tools handle CD.

---

**Q33. Should Jenkins deploy directly to Kubernetes?**
No. Jenkins should update the GitOps repository instead.

---

**Q34. What is Pipeline as Code?**
Defining CI/CD pipelines using version-controlled files.

---

**Q35. How do you secure Jenkins?**
By using RBAC, credentials store, HTTPS, and minimal plugins.

---

## 🔹 Section 4: Advanced & Production (Q36–Q50)

**Q36. What are Jenkins shared libraries?**
Reusable pipeline logic stored in a Git repository.

---

**Q37. Why are shared libraries important?**
They reduce duplication and standardize CI/CD pipelines.

---

**Q38. How does Jenkins handle secrets?**
Using the Jenkins credentials store and secret bindings.

---

**Q39. What is CSRF protection in Jenkins?**
It protects Jenkins from fake POST requests using crumbs.

---

**Q40. How do you handle high load in Jenkins?**
By using agents, limiting plugins, and scaling horizontally.

---

**Q41. How does Jenkins support parallel execution?**
By running multiple stages in parallel.

---

**Q42. Can Jenkins run jobs in parallel?**
Yes, Jenkins supports parallel job execution.

---

**Q43. Jenkins freestyle job vs pipeline job?**
Pipeline jobs are code-based and preferred in production.

---

**Q44. How does Jenkins handle failures?**
Using stage-level error handling and post actions.

---

**Q45. How does Jenkins integrate with Docker?**
Using Docker plugins or Docker-based agents.

---

**Q46. What is Blue Ocean?**
A visual user interface for Jenkins pipelines.

---

**Q47. Is Blue Ocean used in production?**
Rarely. It is mainly used for visualization.

---

**Q48. How do you upgrade Jenkins safely?**
By taking backups, testing plugins, and upgrading carefully.

---

**Q49. How is Jenkins HA achieved?**
Using external storage and a load balancer.

---

**Q50. Biggest mistake beginners make in Jenkins?**
Running builds on the controller.

---

## 🔹 Section 5: Mock Interview (Real Interviewer Style)

**Interviewer:** Explain your Jenkins setup.
**You:** We use Jenkins for CI with Kubernetes-based ephemeral agents. Jenkins builds, tests, performs SAST and image scanning, and updates a GitOps repository for deployment.

---

**Interviewer:** How do you ensure security in Jenkins pipelines?
**You:** By integrating SonarQube for SAST, Trivy for image scanning, enforcing quality gates, and blocking pipelines on critical issues.

---

**Interviewer:** Who deploys to Kubernetes, Jenkins or Argo CD?
**You:** Jenkins never deploys directly. It updates Git, and Argo CD handles deployment.

---

**Interviewer:** Where does Jenkins run in your setup?
**You:** Jenkins runs on Kubernetes, and all builds run on dynamic pod agents.

---

**Interviewer:** What happens if the SonarQube quality gate fails?
**You:** The Jenkins pipeline stops and the image is not promoted.

---

**Interviewer:** Why Kubernetes agents instead of static VMs?
**You:** Kubernetes agents provide better scalability, isolation, and cost efficiency.

---

