# Jenkins Authentication & Authorization – 
---

## 1️⃣ Jenkins Authentication (Who You Are)

### What is Authentication?

Authentication verifies **who is logging in to Jenkins**.

Simple definition:

> Authentication answers the question: *Who are you?*

---

## Authentication Methods Used in Production

### ✅ 1. LDAP / Active Directory (MOST COMMON)

Used in:

* Enterprises
* Corporate environments

Why:

* Central user management
* Easy onboarding/offboarding

---

### ✅ 2. GitHub / GitLab OAuth

Used in:

* Cloud-native teams
* DevOps-focused companies

Why:

* Developers already have accounts
* Easy integration

---

### ✅ 3. SSO (SAML / OIDC)

Used in:

* Large organizations
* Security-heavy environments

Why:

* One login for all tools
* Strong security

---

### ❌ Local Jenkins Users (NOT RECOMMENDED)

* Manual user creation
* Hard to manage

Used only for:

* Lab
* Local testing

---

## Production Authentication Best Practices

* Disable anonymous access
* Integrate with central identity provider
* Enforce strong passwords
* Enable HTTPS

---

## 2️⃣ Jenkins Authorization (What You Can Do)

### What is Authorization?

Authorization controls **what an authenticated user is allowed to do**.

Simple definition:

> Authorization answers the question: *What are you allowed to do?*

---

## Authorization Strategies Used in Production

### ✅ 1. Role-Based Authorization (MOST USED)

Users are assigned roles like:

* Admin
* Developer
* Read-only

Each role has defined permissions.

---

### ✅ 2. Matrix-Based Authorization

* Fine-grained permissions
* User/group-level control

Used when:

* Teams need strict control

---

### ❌ Anyone Can Do Anything (NEVER USE)

* Unsafe
* High risk

---

## Production Authorization Best Practices

* Follow least privilege principle
* Restrict job creation
* Restrict production deployments
* Separate admin and developer roles

---

## Authentication vs Authorization (Easy Table)

| Authentication | Authorization   |
| -------------- | --------------- |
| Who you are    | What you can do |
| Login          | Permissions     |
| Identity       | Access level    |

---

