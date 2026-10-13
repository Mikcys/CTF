# 🏨 Complimentary

## 🎯 Challenge Overview
* **Category:** Cloud Security / AWS Misconfiguration & API Exploitation
* **Target:** `complimentary-GuestWellnessProfiles` DynamoDB Table via AWS Cognito Identity Pool

---

## 🔍 Initial Reconnaissance & Analysis

Upon navigating to the target web application, we inspect the client-side JavaScript source code (`app.js`) using Browser Developer Tools (`F12`). 

Looking through the source code, we locate an unauthenticated **AWS Cognito Identity Pool configuration** hardcoded in the frontend:
Use the source code to find necessary details
Commands:
bash
aws configure
aws dynamodb
aws dynamodb scan --table-name "table name"



