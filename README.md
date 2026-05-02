# 📧 Smart Email-Based Invoice Tracker & Reminder System (n8n)

> An automated system to track sent and received invoices via Gmail and send reminders using n8n workflows and Google Sheets.

---

## 🚀 Project Overview

Managing invoices manually can lead to missed payments and delays. This project automates invoice tracking by monitoring Gmail activity and maintaining a centralized log in Google Sheets.

The system automatically:
- Detects invoice-related emails (sent & received)
- Stores relevant details in a structured format
- Runs a daily scheduler to send reminders
- Differentiates between outgoing invoices and incoming bills

---

## ✨ Features

✅ Tracks **sent invoices** (client payments)  
✅ Tracks **received invoices** (your bills)  
✅ Uses Gmail search filters for efficient detection  
✅ Stores structured data in Google Sheets  
✅ Runs **daily reminder automation (Cron-based)**  
✅ Sends:
- 📤 Client reminders for unpaid invoices  
- 📥 Personal reminders for incoming bills  
✅ Uses **Switch-based routing logic** (advanced workflow design)

---

## 🧠 Workflow Architecture

### 🔹 Workflow 1: Sent Email Tracker
- Trigger: Gmail (Sent folder)
- Filter: `subject:(invoice OR payment)`
- Extracts:
  - Email (recipient)
  - Subject
  - Date
  - Status = Pending
- Stores data in Google Sheets

---

### 🔹 Workflow 2: Incoming Email Tracker
- Trigger: Gmail (Inbox, unread)
- Filter: `subject:(invoice OR payment)`
- Extracts:
  - Sender email
  - Subject
  - Date
  - Status = Pending
- Stores data in Google Sheets

---

### 🔹 Workflow 3: Reminder System
- Trigger: Daily Schedule (9 AM)
- Reads all records from Google Sheets
- Filters:
  - STATUS = Pending
- Routes using **Switch Node**:
  - OUTGOING → Send reminder to client
  - INCOMING → Send reminder to self

---

## 🔄 Workflow Logic

```text
Gmail Trigger (Sent/Inbox)
        ↓
    Data Extraction
        ↓
 Google Sheets Storage
        ↓
 Daily Cron Trigger
        ↓
 Filter Pending Records
        ↓
    Switch by Direction
   ↙              ↘
Outgoing        Incoming
 ↓               ↓
Client Email   Self Reminder
 ↓               ↓
Notification   Notification
```

---

## 🛠️ Tech Stack

* ⚙️ n8n (Cloud)
* 📧 Gmail API
* 📊 Google Sheets API
* ⏰ Cron Scheduler

---

## 📊 Data Structure

| DATE       | TYPE | EMAIL                                   | AMOUNT | DueDate | STATUS  |
| ---------- | ---- | --------------------------------------- | ------ | ------- | ------- |
| 2026-05-01 | sent | [client@gmail.com](mailto:client@gmail.com) | 0      |         | Pending |

---

## ⚙️ Setup Instructions

### 1. Import Workflow

* Open n8n
* Click **Import Workflow**
* Upload JSON file

---

### 2. Connect Credentials

* Connect Gmail (OAuth2)
* Connect Google Sheets

---

### 3. Configure Google Sheet

Create a sheet:

```
InvoiceTrackerTest
```

Columns:

```
DATE | TYPE | EMAIL | AMOUNT | DueDate | STATUS
```

---

### 4. Activate Workflows

* Enable all workflows
* Test using:

```
Subject: Invoice for Project
```

---

## 🧪 Testing

### ✔ Test Sent Emails

Send email:

```
yourmain → client
Subject: Invoice
```

---

### ✔ Test Incoming Emails

Send:

```
client → yourmain
Subject: Payment Due
```

---

### ✔ Test Reminder System

* Run workflow manually
* Verify reminder emails

---

## ⚠️ Known Limitations

* Amount and DueDate are not automatically extracted
* Relies on subject keywords
* No duplicate email prevention
* No reminder frequency control

---

## 🔮 Future Improvements

* 🤖 AI-based extraction (amount, due date)
* 📎 PDF invoice parsing
* 🔁 Smart reminder intervals
* 📊 Dashboard analytics
* 🔐 Status update automation

---

## 🎯 Learning Outcomes

* Event-driven automation using n8n
* API integration (Gmail + Google Sheets)
* Workflow design using Switch logic
* Real-world problem solving

---

## 👨‍💻 Author

Your Name  
GitHub: [https://github.com/yourusername](https://github.com/yourusername)
