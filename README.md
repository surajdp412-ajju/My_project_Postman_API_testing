# 🚀 My_Projects — API Test Collection

A professional end-to-end API testing project built using

* Postman
* REST API Testing
* Environment Variables
* Automated Request Chaining
* Collection Runner
* Newman CLI
* GitHub Version Control
* CI/CD Ready Automation

This project demonstrates a complete API testing workflow using the ReqRes REST API and showcases practical API automation techniques commonly used in real-world QA and Software Testing projects.

---

# 📌 Project Overview

The **My_Projects API Test Collection** is designed to simulate a real-world API testing lifecycle.

The collection is divided into two structured testing modules:

1. Authorization & Authentication Testing
2. End-to-End User Flow Automation

The project validates:

* API authentication flows
* Token generation and reuse
* CRUD operations
* Dynamic environment variable handling
* Automated request chaining
* Response validations
* Status code validations
* Negative testing
* Collection execution using Postman Runner
* Automation execution using Newman
* CI/CD pipeline readiness

---

# 🏗️ Project Architecture

```text
My_Projects
│
├── collections/
│   └── My_Projects.postman_collection.json
│
├── environments/
│   └── Environment_Testing_2.postman_environment.json
│
├── reports/
│   └── newman-report.html
│
├── screenshots/
│
├── README.md
│
└── .github/
    └── workflows/
        └── postman-api-tests.yml
```

---

# 📂 Collection Structure

```text
My_Projects
├── Authorization and Authentication/
│   ├── Login
│   │    └── POST {{baseURL}}/api/login
│   │
│   └── Get User
│        └── GET {{baseURL}}/api/users?page=2
│
└── User Flow Automation/
    ├── Login (extract token)
    │    └── POST {{baseUrl}}/api/login
│
    ├── Create User
    │    └── POST {{baseUrl}}/api/users
│
    ├── Update User
    │    └── PUT {{baseUrl}}/api/users/{{userId}}
│
    └── Delete User
         └── DELETE {{baseUrl}}/api/users/{{userId}}
```

---

# 🔐 Module 1 — Authorization and Authentication

This module demonstrates API authentication workflows using bearer token authorization.

## ✅ Workflow

### 1. Login Request

* Authenticates the user
* Sends credentials to the API
* Validates successful login
* Extracts bearer token from response
* Stores token into environment variable:

```javascript
pm.environment.set("token", response.token)
```

---

### 2. Get User Request

* Uses stored bearer token
* Sends authenticated GET request
* Retrieves paginated users
* Performs extensive response validation

---

## ✅ Validation Coverage

### Positive Validations

* Status code validation
* Token validation
* Response time validation
* Response schema validation
* User data validation
* Header validation
* Authentication validation

### Negative Validations

* Invalid credentials
* Empty request body
* Missing fields
* Invalid token handling

---

# ⚙️ Module 2 — User Flow Automation

This module demonstrates a fully automated end-to-end API workflow.

The requests are chained dynamically using Postman environment variables.

---

# 🔄 Automated Workflow

```text
Login
   ↓
Extract Token
   ↓
Create User
   ↓
Extract userId
   ↓
Update User
   ↓
Delete User
   ↓
Cleanup Variables
```

---

## Step 1 — Login

### Purpose

Authenticates user and extracts bearer token.

### Environment Variable Created

```text
{{token}}
```

### Sample Script

```javascript
const response = pm.response.json();
pm.environment.set("token", response.token);
```

---

## Step 2 — Create User

### Purpose

Creates a new user dynamically.

### Environment Variable Created

```text
{{userId}}
```

### Sample Script

```javascript
const response = pm.response.json();
pm.environment.set("userId", response.id);
```

---

## Step 3 — Update User

### Purpose

Updates user details using dynamically stored userId.

### Endpoint

```http
PUT {{baseUrl}}/api/users/{{userId}}
```

---

## Step 4 — Delete User

### Purpose

Deletes the dynamically created user.

### Cleanup

```javascript
pm.environment.unset("userId");
```

---

# 🌍 Environment Variables

This project uses the **Environment Testing 2** environment.

| Variable     | Type   | Description                          |
| ------------ | ------ | ------------------------------------ |
| {{baseUrl}}  | string | Base API URL                         |
| {{token}}    | secret | Bearer token extracted from Login    |
| {{userId}}   | string | Dynamic user ID                      |
| {{time now}} | string | Timestamp generated during execution |

---

# 🔑 Authentication

All secured requests use:

```http
Authorization: Bearer {{token}}
```

Additionally, the ReqRes API requires:

```http
x-api-key
```

header in requests.

---

# ▶️ How to Execute the Collection

## Option 1 — Using Postman Collection Runner

### Step 1

Select:

```text
Environment Testing 2
```

---

### Step 2

Ensure:

```text
{{baseUrl}} = https://reqres.in
```

---

### Step 3

Open:

```text
Collection Runner
```

---

### Step 4

Select:

```text
My_Projects Collection
```

---

### Step 5

Click:

```text
Run Collection
```

---

# 🧪 Test Coverage Summary

| Request               | Positive Tests | Negative Tests |
| --------------------- | -------------- | -------------- |
| Login (Auth Folder)   | 8              | 4              |
| Get User              | 15             | 6              |
| Login (Extract Token) | 7              | 4              |
| Create User           | 9              | 4              |
| Update User           | 9              | 4              |
| Delete User           | 6              | 4              |

---

# 📊 Total Testing Scope

## Included Testing Types

✅ Functional Testing

✅ API Testing

✅ Authentication Testing

✅ CRUD Operation Testing

✅ Environment Variable Testing

✅ Response Validation

✅ Negative Testing

✅ Automation Workflow Validation

✅ Request Chaining

✅ Regression Testing

✅ Smoke Testing

✅ Collection Runner Execution

✅ Newman Automation

✅ CI/CD Integration Ready

---

# 📦 Newman Automation

This project is fully compatible with Newman CLI for command-line automation.

---

# ⚡ Install Newman

```bash
npm install -g newman
```

---

# ▶️ Run Collection Using Newman

```bash
newman run collections/My_Projects.postman_collection.json \
-e environments/Environment_Testing_2.postman_environment.json
```

---

# 📄 Generate HTML Report

Install reporter:

```bash
npm install -g newman-reporter-html
```

Run:

```bash
newman run collections/My_Projects.postman_collection.json \
-e environments/Environment_Testing_2.postman_environment.json \
-r cli,html
```

---

# 🔁 CI/CD Integration

This project is designed to support CI/CD execution.

Supported platforms:

* GitHub Actions
* Jenkins
* Azure DevOps
* GitLab CI/CD

---

# 🚀 GitHub Actions Example

Create:

```text
.github/workflows/postman-api-tests.yml
```

---

## Sample Workflow

```yaml
name: Postman API Automation

on:
  push:
    branches:
      - main

jobs:
  api-tests:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Install Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'

      - name: Install Newman
        run: npm install -g newman

      - name: Run Postman Collection
        run: |
          newman run collections/My_Projects.postman_collection.json \
          -e environments/Environment_Testing_2.postman_environment.json
```

---

# 🛡️ Security Best Practices

Before pushing collections to GitHub:

❌ Remove:

* Tokens
* Passwords
* API Keys
* Secrets
* Bearer Tokens

Use placeholder values instead.

---

# 📈 Future Enhancements

The project can be further extended with:

* Data-driven testing
* CSV/JSON external datasets
* OAuth 2.0 authentication
* Advanced schema validation
* Performance testing
* Docker integration
* Jenkins pipeline automation
* Parallel execution
* Dynamic test data generation
* API mocking
* Contract testing

---

# 🧰 Technologies Used

| Tool           | Purpose              |
| -------------- | -------------------- |
| Postman        | API Testing          |
| Newman         | CLI Automation       |
| GitHub         | Version Control      |
| GitHub Actions | CI/CD Automation     |
| ReqRes API     | Mock REST API        |
| JavaScript     | Postman Test Scripts |

---

# 📚 API Reference

This project uses the publicly hosted ReqRes REST API.

Base URL:

```text
https://reqres.in
```

ReqRes provides:

* Authentication APIs
* CRUD APIs
* Mock responses
* REST endpoints for testing and prototyping

---

# 👨‍💻 Author

**Suraj D P**

Senior Delivery Consultant | API Tester | Manual QA Engineer

Specializations:

* API Testing
* Manual Testing
* Healthcare Testing
* Functional Testing
* Automation Readiness
* Postman & Newman
* Agile QA Processes

---

# ⭐ Project Highlights

✅ End-to-End API Workflow

✅ Dynamic Environment Variables

✅ Automated Request Chaining

✅ CI/CD Ready

✅ Newman Automation Compatible

✅ GitHub Integration

✅ Real-world QA Workflow Demonstration

✅ Recruiter-Friendly API Testing Portfolio Project

---

# 📌 Conclusion

This project demonstrates a practical, industry-oriented API testing framework using Postman and Newman.

It showcases real-world QA automation workflows including authentication handling, dynamic request chaining, CRUD operation testing, environment variable management, automation execution, and CI/CD integration readiness.

The project is structured to reflect professional API testing standards commonly followed in enterprise-level software quality engineering teams.
