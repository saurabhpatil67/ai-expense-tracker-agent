# System Design

## Project Overview

AI Expense Tracker Agent is an AI-powered personal finance automation system that enables users to track daily expenses directly through Telegram using natural language or receipt images. The system leverages Gemini AI to extract structured expense information, stores transaction data in Firebase Firestore, monitors monthly spending against user-defined budgets, and automatically generates monthly financial reports.

Unlike traditional expense tracking applications that require manual form filling, this solution provides a conversational interface through Telegram, making expense management faster and more intuitive.

---

## Problem Statement

Traditional expense tracking applications often require users to manually enter transaction details, categorize expenses, and maintain records consistently. This repetitive process reduces user engagement and often results in incomplete financial tracking.

The objective of this project is to simplify expense management by combining conversational interfaces, artificial intelligence, workflow automation, and cloud databases into a single automated solution.

---

## Objectives

- Simplify daily expense tracking.
- Eliminate manual data entry.
- Extract expense information using AI.
- Monitor monthly spending in real time.
- Generate automated monthly reports.
- Visualize spending patterns through charts.
- Deliver all interactions through Telegram.
- Build a scalable workflow using n8n.

---

# Functional Requirements

The system must:

- Register new users.
- Allow users to configure monthly spending limits.
- Accept expense records as text messages.
- Accept receipt images for AI-based extraction.
- Extract structured expense information using Gemini AI.
- Validate extracted information before storage.
- Store expense records securely.
- Track monthly spending.
- Notify users when budget limits are exceeded.
- Generate monthly expense reports automatically.
- Create category-wise pie charts.
- Deliver reports directly through Telegram.

---

# Non-Functional Requirements

- Fast response time.
- High workflow reliability.
- Modular architecture.
- Scalable database design.
- Maintainable workflow logic.
- Cloud-based storage.
- Easy future expansion.

---

# High-Level System Design

The system consists of two independent automation workflows.

**Workflow 1**
- Handles user interaction.
- Records expenses.
- Validates AI output.
- Stores transactions.
- Tracks monthly budget.

**Workflow 2**
- Executes automatically every month.
- Retrieves previous month's expenses.
- Generates analytics.
- Creates spending charts.
- Sends monthly reports.

This separation improves maintainability, scalability, and simplifies future enhancements.

---

# Core Components

## Telegram Bot

Acts as the primary user interface where users:

- Register
- Configure limits
- Record expenses
- Receive notifications
- Receive monthly reports

---

## Gemini AI

Responsible for understanding:

- Natural language
- Receipt images

Gemini converts unstructured input into structured expense information.

---

## Firebase Firestore

Stores:

- User budget configuration
- Expense transactions

Firestore provides scalable cloud storage with efficient document retrieval.

---

## n8n

Serves as the automation engine responsible for:

- Workflow execution
- API integrations
- AI communication
- Database operations
- Scheduled automation
- Business logic

---

## QuickChart

Generates category-wise pie charts for monthly expense visualization.

---

# AI Processing Pipeline

The expense processing pipeline follows these stages:

1. User submits expense.
2. Telegram forwards the message.
3. Gemini AI extracts structured data.
4. Validation verifies extracted fields.
5. Firestore stores the transaction.
6. Monthly spending is recalculated.
7. Budget status is evaluated.
8. Telegram sends confirmation.

---

# Security Considerations

The system follows several design practices to improve data safety.

- User data is isolated using Telegram User ID.
- Monthly limits are stored separately from expenses.
- Validation prevents incomplete records.
- Scheduled reports access only authorized user data.
- No sensitive credentials are exposed to users.

---

# Scalability

The architecture supports future growth by:

- Separating workflows by responsibility.
- Using Firestore's scalable document database.
- Processing users independently during report generation.
- Allowing additional workflows without affecting existing logic.
- Supporting future AI model replacement with minimal workflow changes.

---

# Current Limitations

- Single currency support.
- Telegram-only interface.
- No recurring expense detection.
- No web dashboard.
- No OCR confidence scoring.
- No offline capability.

---

# Future Enhancements

Potential improvements include:

- Voice-based expense logging.
- Multi-language support.
- Multi-currency support.
- Weekly reports.
- Spending prediction using AI.
- Merchant analytics.
- Interactive dashboard.
- Mobile application.
- PDF report generation.
- Advanced financial insights.

---

# Conclusion

The AI Expense Tracker Agent combines conversational interfaces, workflow automation, artificial intelligence, and cloud databases to create an intelligent expense management solution. By separating real-time expense tracking from scheduled reporting, the architecture remains modular, scalable, and easy to maintain while providing a seamless user experience through Telegram.
