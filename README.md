# Smart Leave & Absence Management Engine

## 📌 Overview

The Smart Leave & Absence Management Engine is a production-style serverless leave management system built on AWS. The application allows employees to apply for leave, managers and HR teams to approve or reject requests through a structured workflow, and automatically manages leave balances, notifications, and scheduled processing.

The system supports multiple leave types such as Casual Leave, Sick Leave, Earned Leave, and Unpaid Leave with configurable quota management.

---

# 🚀 Features

## ✅ Employee Features

* Secure login using Amazon Cognito
* Apply leave through web interface
* View leave history and request status
* View leave balances
* Automatic rejection for insufficient balance
* Overlapping leave request detection

## ✅ Manager Features

* View pending leave requests
* Approve or reject leave requests
* Multi-level approval support

## ✅ HR Features

* HR dashboard with:

  * Pending requests
  * Approved requests
  * Rejected requests
  * Team absence calendar
* Download leave reports as CSV
* Final approval for long-duration leaves

## ✅ Automation Features

* Weekly leave balance processing
* Automated carry-forward logic
* Automated leave balance summary emails
* Event-driven workflows using AWS services

---

# 🏗️ AWS Services Used

| Service            | Purpose                        |
| ------------------ | ------------------------------ |
| Amazon Cognito     | Authentication & Authorization |
| Amazon S3          | Frontend hosting               |
| Amazon CloudFront  | CDN & HTTPS delivery           |
| Amazon API Gateway | REST API endpoints             |
| AWS Lambda         | Backend business logic         |
| AWS Step Functions | Multi-level approval workflow  |
| Amazon DynamoDB    | Data storage                   |
| Amazon SES         | Email notifications            |
| Amazon EventBridge | Scheduled automation           |
| Amazon SNS         | Manager notifications          |

---

# 🧠 System Workflow

## Employee Leave Request Flow

1. Employee logs in using Amazon Cognito
2. Employee submits leave request from React frontend
3. API Gateway invokes Lambda function
4. Lambda validates:

   * Leave balance
   * Overlapping leave requests
5. Request stored in DynamoDB
6. Step Functions starts approval workflow
7. SNS/SES sends manager notification
8. Manager approves/rejects request
9. If leave > 5 days → HR approval required
10. Final status stored in DynamoDB
11. Employee receives SES email notification
12. Leave balance updated after final approval

---

# 📂 Project Architecture

## Frontend

* React + Vite
* Hosted on Amazon S3
* Distributed via CloudFront
* Cognito authentication integration

## Backend

* API Gateway endpoints
* AWS Lambda functions for:

  * Leave application
  * Approval processing
  * HR processing
  * Weekly leave balance automation

## Database

### DynamoDB Tables

### 1. lms-leave-requests-dev

| Attribute   | Description      |
| ----------- | ---------------- |
| employee_id | Partition key    |
| request_id  | Sort key         |
| leave_type  | Type of leave    |
| start_date  | Leave start date |
| end_date    | Leave end date   |
| status      | Current status   |

### 2. lms-leave-balances-dev

| Attribute   | Description          |
| ----------- | -------------------- |
| employee_id | Partition key        |
| casual      | Casual leave balance |
| sick        | Sick leave balance   |
| earned      | Earned leave balance |

### 3. lms-leave-config-dev

| Attribute    | Description  |
| ------------ | ------------ |
| leave_type   | Leave type   |
| annual_quota | Annual quota |

---

# 🔄 Step Functions Workflow

## Approval Logic

### Leave ≤ 5 Days

Employee → Manager Approval → Final Approval

### Leave > 5 Days

Employee → Manager Approval → HR Approval → Final Approval

---

# ⏰ EventBridge Automation

Amazon EventBridge triggers a scheduled Lambda function weekly to:

* Process leave balances
* Apply carry-forward logic
* Send leave balance summary emails using SES

---

# 📧 Email Notifications

Amazon SES is used to send:

* Leave submission confirmation
* Manager approval/rejection notifications
* HR approval notifications
* Weekly leave balance summaries

---

# 🛡️ Edge Cases Handled

✅ Insufficient leave balance

✅ Overlapping leave requests

✅ Multi-level approval for long leaves

✅ Authentication & authorization

✅ Automated balance updates

---

# 📊 Screenshots To Include In GitHub

Add screenshots for:

* Employee dashboard
* HR dashboard
* Leave approval flow
* Step Functions execution
* SES email notification
* DynamoDB tables
* EventBridge scheduler

---

# ⚙️ Setup Instructions

## 1. Clone Repository

```bash
git clone <your-github-repo-url>
cd smart-leave-management-engine
```

## 2. Install Frontend Dependencies

```bash
npm install
```

## 3. Run Frontend

```bash
npm run dev
```

## 4. Configure AWS Services

Create and configure:

* Amazon Cognito
* API Gateway
* Lambda Functions
* DynamoDB Tables
* Step Functions
* SES
* EventBridge
* S3 + CloudFront

---

# 📌 Future Improvements

* Manager inactivity escalation after 48 hours
* Slack/MS Teams notifications
* PDF report generation
* Mobile responsive UI improvements
* Terraform/IaC deployment
* CI/CD pipeline using CodePipeline

---

# 🧑‍💻 Author

Rahul K

GitHub: [https://github.com/rahulrahu15](https://github.com/rahulrahu15)

---

# 🏁 Conclusion

The Smart Leave & Absence Management Engine demonstrates a real-world serverless architecture using AWS services and showcases authentication, workflow orchestration, event-driven automation, frontend hosting, and cloud-native design principles.

This project was built as a production-style full-stack cloud application with scalability, automation, and maintainability in mind.
