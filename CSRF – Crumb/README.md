# Jenkins CSRF – Crumb 
## What is CSRF?

**CSRF (Cross-Site Request Forgery)** is a security attack where:

* A user is logged in to Jenkins
* A malicious request is sent without the user knowing
* Jenkins executes that request because the user is authenticated

Example risk:

* Triggering a build
* Deleting a job
* Changing Jenkins config

---

## Why Jenkins Needs CSRF Protection

Jenkins has:

* Web UI
* REST APIs
* Build triggers

Without protection, **any authenticated browser session could be abused**.

So Jenkins enables **CSRF protection by default**.

---

## What is a Jenkins Crumb?

A **Crumb** is:

* A **security token**
* Added to HTTP requests
* Used to prove the request is **legitimate**

Simple definition:

> A Jenkins crumb is a CSRF token that Jenkins uses to verify requests.

---

## How Jenkins Crumb Works (Step by Step)

1. User logs in to Jenkins
2. Jenkins generates a **crumb**
3. Crumb is tied to:

   * User session
   * IP (optional)
4. Any POST / API request must include the crumb
5. Jenkins verifies the crumb
6. Request is accepted or rejected

If crumb is missing or invalid → ❌ request blocked

---

## Where the Crumb Is Used

Crumbs are required for:

* POST requests
* API calls
* Job triggers via scripts

Not required for:

* Simple GET requests

---

## How Crumb Is Sent

Crumb is sent as an **HTTP header**.

Example:

```
Jenkins-Crumb: abc123xyz
```

---

## Real Example (API Trigger)

Without crumb:

* Jenkins returns **403 Forbidden**

With crumb:

* Request succeeds

This is why scripts sometimes fail with 403 errors.

---

## How to Get a Jenkins Crumb (Concept)

Jenkins exposes an API endpoint to fetch a crumb.

Scripts usually:

1. Call Jenkins crumb API
2. Store the crumb
3. Use it in next request

---

## Should We Disable CSRF / Crumb?

❌ **NO (Not in production)**

Disabling CSRF:

* Makes Jenkins vulnerable
* Is a security risk

Only acceptable:

* Local testing
* Temporary debugging

---

## Common Problems You Will See

### Problem

403 Forbidden when triggering job via API

### Reason

Crumb missing or invalid

### Fix

* Fetch crumb
* Send it in request header

---

