# Database Design

## Overview

The AI Expense Tracker Agent uses **Firebase Firestore** as its cloud-based NoSQL database. Firestore provides scalable document storage, real-time data access, and seamless integration with the automation workflows built in n8n.

The database is organized into two independent collections to separate user configuration from transaction data, improving maintainability and simplifying data retrieval.

---

# Database Architecture


<p align="center">
  <img src="../assets/firestore-er-diagram.png" alt="Firestore ER Diagram" width="100%">
</p>

---

# Database Collections

The application uses two primary collections.

| Collection | Purpose |
|------------|---------|
| limits | Stores monthly budget information for each user |
| expenses | Stores all expense transactions |

---

# Collection: limits

This collection stores each user's monthly spending limit.

## Document Structure

| Field | Type | Description |
|------|------|-------------|
| userId | String | Telegram User ID |
| name | String | User name |
| monthlyLimit | Number | Monthly spending limit |
| createdAt | Timestamp | Record creation time |
| updatedAt | Timestamp | Last updated time |

---

### Example Document

```json
{
  "userId": "987654321",
  "name": "John Doe",
  "monthlyLimit": 1000,
  "createdAt": "2026-07-01T09:00:00Z",
  "updatedAt": "2026-07-01T09:00:00Z"
}
```

<p align="center">
  <img src="../assets/firebase-limit.png" alt="Firebase limit collection diagram" width="100%">
</p>


---

# Collection: expenses

This collection stores every expense recorded by the user.

## Document Structure

| Field | Type | Description |
|------|------|-------------|
| userId | String | Telegram User ID |
| amount | Number | Expense amount |
| category | String | Expense category |
| merchant | String | Merchant name |
| paymentMethod | String | Payment method |
| expenseDate | Timestamp | Date of transaction |
| createdAt | Timestamp | Record creation time |

---

### Example Document

```json
{
  "userId": "987654321",
  "amount": 18.50,
  "category": "Food",
  "merchant": "Star Cafe",
  "paymentMethod": "UPI",
  "expenseDate": "2026-07-25",
  "createdAt": "2026-07-25T18:10:00Z"
}
```

<p align="center">
  <img src="../assets/firebase-expenses.png" alt="Firebase expenses collection diagram" width="100%">
</p>

---

# Relationship Between Collections

The two collections are linked using the **userId** field.

```text
limits
--------
userId
monthlyLimit
name

        │
        │ userId
        ▼

expenses
---------
userId
amount
category
merchant
paymentMethod
expenseDate
```

A single user has one monthly budget configuration and can have multiple expense records.

---

# Data Flow

## Setting Monthly Limit

1. User sends the `/setlimit` command.
2. Workflow validates the input.
3. Firestore creates or updates the document in the `limits` collection.
4. Confirmation is sent to the user.

---

## Recording an Expense

1. User sends an expense through Telegram.
2. Gemini AI extracts structured data.
3. Workflow validates the extracted information.
4. Expense is stored in the `expenses` collection.
5. Monthly spending is recalculated.

---

## Monthly Report Generation

1. Scheduler starts Workflow 2.
2. Registered users are retrieved.
3. Previous month's expenses are fetched.
4. Analytics are calculated.
5. Report is generated and delivered through Telegram.

---

# Query Strategy

The application performs several common database operations.

| Operation | Collection |
|-----------|------------|
| Fetch user budget | limits |
| Update monthly limit | limits |
| Store expense | expenses |
| Retrieve monthly expenses | expenses |
| Calculate category totals | expenses |
| Generate monthly report | expenses |

---

# Database Design Decisions

Several design choices were made to improve performance and maintainability.

### Separate Collections

Budget information and expense records are stored independently to simplify updates and reduce unnecessary data duplication.

### User-Based Data Isolation

Each document is associated with a unique Telegram `userId`, ensuring that every user's data remains isolated.

### Timestamp-Based Records

Timestamps are stored to support monthly filtering, report generation, and future analytics.

### Flexible Schema

Firestore's document model allows additional fields to be added without requiring database migrations.

---

# Advantages of Firestore

- Cloud-managed database
- Automatic scalability
- No server maintenance
- Flexible document model
- Fast document retrieval
- Easy integration with n8n
- Suitable for AI automation workflows

---

# Security Considerations

The database design follows several security practices.

- Data is separated by userId.
- Budget configuration is isolated from expense records.
- Invalid records are rejected before storage.
- Sensitive credentials are never stored inside user documents.

---

# Current Limitations

- No historical budget versions
- No recurring expense records
- No soft delete mechanism
- No audit logging
- Single-currency storage

---

# Future Improvements

Potential database enhancements include:

- Recurring expense collection
- Budget history tracking
- Merchant collection
- Category collection
- OCR confidence storage
- Receipt image metadata
- Multi-currency support
- Spending prediction data
- User preferences collection

---

# Conclusion

The Firestore database is designed to provide a simple, scalable, and maintainable storage layer for the AI Expense Tracker Agent. By separating user budget settings from expense transactions, the system supports efficient querying, easier maintenance, and future feature expansion while remaining well-suited for cloud-based AI automation.
