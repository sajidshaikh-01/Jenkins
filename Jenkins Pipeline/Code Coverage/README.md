
# Code Coverage – Complete DevOps & CI/CD Guide

## 1. What is Code Coverage?

Code coverage is a **metric** that measures how much of your application source code is executed when automated tests run.

In simple words:

> Code coverage tells us **which part of the code is tested and which part is not**.

It is usually represented as a **percentage (%)**.

Example:

* Total lines of code: 100
* Lines executed during tests: 75
* Code Coverage: **75%**

---

## 2. Why Code Coverage is Important (Why We Use It)

### In Production & CI/CD Pipelines

We use code coverage to:

* Ensure **critical business logic is tested**
* Detect **uncovered / risky code paths**
* Improve **code quality and reliability**
* Prevent **untested code** from going to production
* Maintain **engineering standards** across teams

### Interview-ready Explanation

> "Code coverage helps us understand test effectiveness and prevents untested code from being promoted to higher environments."

---

## 3. What Code Coverage is NOT ❌

Important to understand:

* ❌ High coverage does NOT guarantee bug-free code
* ❌ Coverage does NOT test code correctness
* ❌ 100% coverage does NOT mean perfect testing

Code coverage measures **execution**, not **quality of assertions**.

---

## 4. Types of Code Coverage

### 1️⃣ Line Coverage

Measures how many lines of code are executed.

Example:

```text
Executed lines / Total lines
```

Used mostly in:

* Java
* Python
* JavaScript

---

### 2️⃣ Statement Coverage

Checks whether each statement in the code is executed at least once.

Slightly more accurate than line coverage.

---

### 3️⃣ Function / Method Coverage

Measures whether functions or methods are called during tests.

Useful for:

* API services
* Microservices

---

### 4️⃣ Branch Coverage (VERY IMPORTANT)

Measures whether all branches of conditional logic are tested.

Example:

```java
if (x > 10) {
   // true branch
} else {
   // false branch
}
```

Both `true` and `false` paths must be tested.

👉 Preferred in **production-grade pipelines**.

---

### 5️⃣ Condition Coverage

Ensures each boolean condition is evaluated as:

* TRUE
* FALSE

Used in:

* Financial systems
* Critical business logic

---

### 6️⃣ Path Coverage (Advanced)

Tests all possible execution paths.

* Very expensive
* Rarely used fully in real-world projects

---

## 5. Common Code Coverage Tools (Production Usage)

### 🔹 Java

* **JaCoCo** (Most popular)
* Cobertura

### 🔹 JavaScript / TypeScript

* Istanbul
* NYC
* Jest built-in coverage

### 🔹 Python

* coverage.py
* pytest-cov

### 🔹 Go

* go test -cover

### 🔹 .NET

* Coverlet

---

## 6. Code Coverage with CI/CD (Jenkins Example)

Typical Jenkins pipeline flow:

```
Code Commit
   ↓
Build
   ↓
Unit Tests + Coverage
   ↓
Coverage Report Generated
   ↓
Quality Gate Check
```

Example (Conceptual):

* Minimum coverage required: **80%**
* If coverage < 80% → Pipeline FAILS

---

## 7. Code Coverage + SonarQube (Production Standard)

In real production environments:

* Tests generate coverage report (JaCoCo / Istanbul)
* SonarQube ingests report
* Quality Gate evaluates:

  * Coverage %
  * Code smells
  * Bugs
  * Vulnerabilities

👉 If Quality Gate fails → **deployment is blocked**.

---

## 8. Best Practices (Production)

* Focus on **critical logic**, not 100% coverage
* Enforce coverage on **new code**, not legacy code
* Use **branch coverage** instead of only line coverage
* Combine coverage with **code reviews**
* Never fake coverage with empty tests

---

