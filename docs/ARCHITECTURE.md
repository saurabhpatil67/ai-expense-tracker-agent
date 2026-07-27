# Architecture

## Overview

The AI Expense Tracker Agent is built using a modular workflow architecture powered by n8n. The system separates real-time expense tracking from scheduled monthly reporting, allowing each workflow to operate independently while sharing the same Firestore database.

This architecture improves maintainability, scalability, and simplifies future feature development.

---

# Architecture Diagram

<p align="center">
  <img src="../assets/architecture.png" alt="System Architecture" width="100%">
</p>

---

# Architecture Components

The solution consists of six major components.

| Component | Responsibility |
|-----------|----------------|
| Telegram Bot | User interaction |
| n8n Workflow 1 | Expense tracking automation |
| Gemini AI | Expense extraction from text and images |
| Firebase Firestore | Persistent data storage |
| n8n Workflow 2 | Monthly report generation |
| QuickChart API | Category-wise chart generation |

---

# Workflow Architecture

The project consists of two independent workflows.

## Workflow 1 — AI Expense Tracking

Responsibilities:

- Receive Telegram messages
- Process commands
- Verify users
- Validate monthly limits
- Extract expense details using Gemini AI
- Validate extracted information
- Store expenses
- Calculate monthly spending
- Monitor budget
- Send confirmation messages

<p align="center">
  <img src="../assets/workflow-1.png" alt="Workflow 1" width="100%">
</p>

---

## Workflow 2 — Monthly Expense Report

Responsibilities:

- Execute automatically every month
- Retrieve registered users
- Fetch previous month's expenses
- Generate analytics
- Create pie charts
- Send reports through Telegram

<p align="center">
  <img src="../assets/workflow-2.png" alt="Workflow 2" width="100%">
</p>

---

# Component Interaction

The following sequence describes how system components interact during expense tracking.

1. User sends a message through Telegram.
2. Telegram forwards the request to n8n.
3. n8n determines the request type.
4. Gemini AI extracts structured expense information.
5. Validation checks extracted fields.
6. Firestore stores the expense.
7. Monthly spending is recalculated.
8. Budget status is evaluated.
9. Telegram receives the final response.

---

# Data Flow

The architecture follows a unidirectional data flow.

```text
Telegram
      │
      ▼
n8n Workflow
      │
      ▼
Gemini AI
      │
      ▼
Validation
      │
      ▼
Firestore
      │
      ▼
Budget Analysis
      │
      ▼
Telegram Response
```

---

# Technology Integration

## Telegram

Provides the conversational interface for all user interactions.

## n8n

Acts as the orchestration layer connecting all external services.

## Gemini AI

Converts unstructured user input into structured expense data.

## Firebase Firestore

Stores user configuration and expense history.

## QuickChart

Creates graphical monthly spending summaries.

---

# Architectural Principles

The architecture follows several design principles.

- Separation of responsibilities
- Modular workflow design
- AI-first data extraction
- Stateless workflow execution
- Scalable cloud storage
- Event-driven automation
- Independent scheduled reporting

---

# Design Advantages

This architecture provides several benefits.

- Easy to maintain
- Easy to extend
- Supports multiple users
- Independent workflows
- Cloud-native storage
- Minimal manual processing
- AI-powered automation
- Reduced system complexity

---

# Future Architecture

The current architecture can be extended by adding:

- Voice processing workflow
- OCR preprocessing workflow
- Email notification workflow
- Web dashboard
- Mobile application
- AI spending prediction
- Multi-language support
- Multi-currency support

---

# Conclusion

The architecture of the AI Expense Tracker Agent emphasizes modularity, automation, and scalability. By separating real-time expense tracking from scheduled monthly reporting, the system remains organized, maintainable, and ready for future enhancements without requiring major architectural changes.
