# Jenkins Security – 
---
## Why Jenkins Security Is Important

Jenkins controls:

* Code builds
* Deployments
* Production access
* Secrets

If Jenkins is compromised:

* Attackers can deploy malicious code
* Secrets can be leaked
* Production systems can be damaged

👉 Jenkins is a **high-value attack target**.

---

## Core Areas of Jenkins Security

In production, Jenkins security is built around **five main areas**:

1. Authentication (Who can log in)
2. Authorization (What they can do)
3. Credentials management
4. CSRF & API protection
5. Agent & network security

---

## 1️⃣ Authentication (High-Level)

* Verifies **identity of users**
* Integrated with company identity systems

Examples:

* LDAP / Active Directory
* GitHub / GitLab OAuth
* SSO (SAML, OIDC)

⚠️ Never allow anonymous access in production.

---

## 2️⃣ Authorization (High-Level)

* Controls **permissions after login**
* Prevents users from doing unsafe actions

Examples:

* Who can create jobs
* Who can deploy to production
* Who can manage Jenkins

⚠️ Always follow **least privilege principle**.

---

## 3️⃣ Credentials Management (Very Important)

### What Jenkins Stores

* API tokens
* Passwords
* SSH keys
* Certificates

### Production Rules

* Never hardcode secrets
* Use Jenkins credentials store
* Restrict credential access
* Rotate secrets regularly

---

## 4️⃣ CSRF Protection (Crumbs)

* Jenkins uses **CSRF crumbs**
* Protects against forged requests
* Enabled by default

❌ Do not disable in production.

---

## 5️⃣ Plugin Security

Plugins run inside Jenkins JVM.

### Production Best Practices

* Install minimum plugins
* Remove unused plugins
* Update plugins carefully
* Test updates in staging

---

## 6️⃣ Agent Security

### Key Points

* Do not run builds on controller
* Use ephemeral agents (Docker / Kubernetes)
* Limit agent permissions
* Avoid SSH root access

---

## 7️⃣ Network & Access Security

* Run Jenkins in private network
* Protect with firewall / security groups
* Use HTTPS (TLS)
* Restrict access to trusted IPs

---

