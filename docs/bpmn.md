# Career Networking Copilot — BPMN / User & Business Process

## 1. Process Objective

Model the end-to-end networking workflow as one continuous process from company discovery through personalized outreach.

The key design principle is **data continuity**: information discovered by AI should become structured product data and flow into downstream outreach without requiring duplicate entry.

## 2. Swimlanes

1. **User**
2. **Career Networking Copilot**
3. **Web / Search**
4. **Database**
5. **External Channel — Email / LinkedIn**

## 3. End-to-End BPMN Flow

~~~text
START
  ↓
User sets / updates preferences
  ↓
AI requests company discovery
  ↓
Web / Search discovers companies
  ↓
AI validates company relevance
(location, industry, domain, company type)
  ↓
Database stores company + source information
  ↓
User reviews discovered companies
  ↓
User selects company
  ↓
AI recommends potential contacts
        ├── User accepts AI recommendation
        │       ↓
        │   Contact record automatically created/pre-populated
        │       ↓
        │   User reviews / corrects / completes
        │
        └── User researches independently
                ↓
            User adds person
                ↓
            Contact record created
                ↓
            User reviews / corrects / completes
                         ↓
                  Contact Record
                         ↓
                  User clicks
                  "Draft Outreach"
                         ↓
              Retrieve relevant context
              ├── Career profile
              ├── Networking preferences
              ├── Company
              ├── Person/contact
              ├── Relevant job, if available
              ├── Writing preferences
              └── Previous outreach, if any
                         ↓
                  Generate message
                         ↓
                  Validate message
                         ↓
                  User reviews / edits
                    ├── Regenerate
                    └── Continue
                         ↓
                 Human approval
                         ↓
              Execute / perform outreach
                 ├── Email
                 └── LinkedIn
                         ↓
              User records status/outcome
                         ↓
                    Database
                         ↓
                 No response?
                  ├── Yes → Reminder
                  │          ↓
                  │     User decides next action
                  └── No → Continue tracking
                         ↓
                        END
~~~

## 4. Critical Handoffs

### Handoff 1 — AI Recommendation → Contact
The accepted recommendation becomes a structured contact record.

Known fields must be carried forward automatically. The user only fills missing information or corrects errors.

### Handoff 2 — Contact → Outreach
The Contact record exposes a **Draft Outreach** action.

The user does not start a disconnected message form or re-enter company/person information.

### Handoff 3 — Contact → AI Context
The system retrieves relevant structured context automatically when Draft Outreach is selected.

### Handoff 4 — Message → Human Approval
The generated message is immediately available for user review/editing before approval.

### Handoff 5 — Outreach → Tracking
The resulting outreach remains associated with the Contact and is stored for future context.

## 5. Decision Points

| Decision | Decision maker |
|---|---|
| Is company relevant? | AI recommends; user reviews |
| Which person to contact? | User |
| Accept AI person recommendation? | User |
| Correct contact information? | User |
| Draft outreach? | User |
| Message content | AI generates; user reviews/edits |
| Send outreach? | User approval required |
| Follow up? | User |
| Change AI classification/priority? | User |

## 6. UX Principle

> **AI recommendation should become structured product data and flow directly into personalized outreach, rather than being displayed and discarded.**

The system should never ask the user to re-enter information already known from an earlier step.
