# Restful Booker API Automation

## Overview

This project automates the Restful Booker APIs using:

- Postman
- Newman
- GitHub Actions

The framework covers CRUD operations (Create, Read, Update, Delete) and negative test scenarios for the Restful Booker application.

---

## Tech Stack

- Postman
- Newman
- Node.js
- GitHub Actions

---

## Project Structure

```text
restful-booker-api-automation
│
├── .github
│   └── workflows
│       └── api-tests.yml
│
├── collections
│   └── Restful-booker.postman_collection.json
│
├── environments
│   └── Restful-booker.postman_environment.json
│
├── reports
│   └── report.html
│
├── package.json
├── package-lock.json
└── README.md
```

---

## Test Coverage

### Positive Test Cases

1. Generate authentication token
2. Get booking IDs
3. Create booking
4. Get booking details
5. Update booking
6. Delete booking
7. Verify API health endpoint

### Negative Test Cases

1. Generate token with invalid credentials
2. Get booking with invalid Booking ID
3. Update booking without token
4. Delete booking without token
5. Update booking with invalid Booking ID
6. Delete booking with invalid Booking ID

---

## Environment Variables

| Variable | Description |
|-----------|-------------|
| Base_URL | API Base URL |
| Token | Authentication Token |
| ID | Generated Booking ID |
| First_Name | Original First Name given while booking|
| Last_Name | Original Last Name given while booking|
| Total_Price | Original Total Price given while booking|
| Update_First_Name | Updated First Name |
| Update_Last_Name | Updated Last Name |
| Update_Total_Price | Updated Total Price |

---
## Prerequisites

Before running the tests, ensure the following are installed:

- Node.js (v18 or higher)
- Visual Studio Code
- Git

Verify installation:

```bash
node -v
npm -v
git --version
```

---

## Running Tests Locally

### Clone Repository

```bash
git clone https://github.com/vaishnavit29/playwright-qa-assignment-API.git
```

### Navigate to Project

```bash
cd playwright-qa-assignment-API
```

### Install Dependencies

```bash
npm install
```

### Execute API Collection

```bash
npm run test:api
```

This command executes all CRUD and negative API test scenarios using Newman.

### Generate HTML Report

```bash
npm run test:report
```

Report Location:

```text
reports/report.html
```

Open the generated report in any browser to review execution results.

---

## CI/CD

GitHub Actions is configured to automatically execute the API test suite on every Pull Request.

Workflow file:

```text
.github/workflows/api-tests.yml
```
---

## Newman Commands

### Run Collection

```bash
npx newman run collections/Restful-booker.postman_collection.json \
-e environments/Restful-booker.postman_environment.json
```

### Run Collection with HTML Report

```bash
npx newman run collections/Restful-booker.postman_collection.json \
-e environments/Restful-booker.postman_environment.json \
-r cli,htmlextra \
--reporter-htmlextra-export reports/report.html
```

---

## CI/CD Integration

GitHub Actions is configured to:

- Trigger on Pull Request
- Install dependencies
- Execute Newman Collection
- Report Pass/Fail status

Workflow file:

```text
.github/workflows/api-tests.yml
```

---

## GitHub Actions Workflow

```yaml
name: API Tests

on:
  push:
  pull_request:

jobs:
  api-tests:

    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-node@v4
        with:
          node-version: 20

      - run: npm install

      - run: npm install -g newman

      - run: newman run collections/Restful-booker.postman_collection.json -e environments/Restful-booker.postman_environment.json
```

---

## Execution Flow

```text
Generate Token
       ↓
Get Bookings  
        ↓
Create Booking
       ↓
Get Booking Details
       ↓
Update Booking
       ↓
Delete Booking
       ↓
Verify Response
```

---

## Author

**Vaishnavi Tandle**

QA Engineer | API Testing | Postman | Newman | Playwright