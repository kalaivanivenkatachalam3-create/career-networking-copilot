# Career Networking Copilot — Product Requirements Document

## 1. Product Objective
Build an AI-powered copilot that helps professionals proactively discover relevant companies, identify potential contacts, create personalized outreach, and track networking activity.

**Core principle:** AI discovers and prepares. The user decides and acts.

## 2. Target User
The primary user is an individual professional seeking to build a career network proactively. The MVP is single-user.

## 3. MVP User Journey
Preferences → Discover Companies → Review → Identify/Add People → Draft Outreach → Approve → Outreach → Track

## 4. Functional Requirements

### FR1 — Career & Networking Preferences
The user can configure career profile, resume/profile, experience, skills, career positioning, industry, domain, company type, preferred locations, target roles, writing preferences and daily outreach limit. Preferences are persisted for future discovery and personalization.

### FR2 — Company Discovery
The system discovers companies based on user preferences. Capture company name, website, industry/domain, company type, presence in preferred location(s), relevant information, open jobs if available, and source. Open jobs are informational, not a prerequisite. The MVP presents discovered companies and does not automatically rank them.

### FR3 — People Identification
The system may recommend HR/Talent Acquisition, relevant Product leaders, or people in closely related roles. Location relevance can influence recommendations but is not a mandatory filter. The user can select an AI-recommended person or add a person discovered independently.

### FR4 — Contact Management
Store full name, email, position, company, role/job ID, profile URL, contact type, channel, tailored resume, outreach status, last contacted date, next reminder, message history, outcome and notes.

### FR5 — Personalized Outreach
Generate personalized Email and LinkedIn messages using career profile, writing preferences, company context, person context and relevant previous outreach. For LinkedIn, the user provides the character limit before generation.

### FR6 — Human Approval
External outreach follows: AI Draft → User Review/Edit → User Approval → Outreach. No external message is sent without user approval. For LinkedIn MVP, the system prepares the message and the user performs the LinkedIn action.

### FR7 — Daily Outreach Limit
The user configures a daily outreach limit. When reached, do not suggest additional outreach for that day; carry remaining opportunities forward; allow the user to change the limit.

### FR8 — Outreach Tracking
Suggested statuses: Not Contacted → Drafted → Approved → Sent → Responded → No Response → Interested → Not Interested → Closed. The user can record date, channel, response summary, notes, next action, reminder and outcome. AI must not assume an external action or response occurred.

### FR9 — Follow-up Reminder
The system can remind the user when a contact has not responded. It does not automatically send follow-ups. The user decides whether to follow up, find another contact, or close the opportunity.

### FR10 — AI Correctability
For AI-generated classification or prioritization, the user can accept the AI decision, change classification, change priority, and optionally provide a correction reason. Record the original AI decision and final human decision as an evaluation signal.

## 5. Non-Functional Requirements
- **Privacy:** Store career profile and outreach information securely.
- **Explainability:** Where practical, show why a company or person was considered relevant.
- **Traceability:** AI-generated decisions and human corrections should be auditable.
- **Reliability:** Consequential external actions require explicit user approval.
- **Context efficiency:** The LLM receives relevant retrieved context rather than the entire database.

## 6. Data Principle
**Database = persistent source of truth.**
**AI context = information retrieved for the current task.**

## 7. Success Metrics

### User / Business Outcome
- Relevant companies discovered
- Relevant contacts identified
- Outreach sent
- Response rate
- Interested-contact rate

### AI Quality
- Messages accepted without edits
- Messages edited
- Messages rejected
- AI decisions corrected

### Productivity
- Time saved per outreach
- Outreach consistency
- Daily limit adherence

### North-star question
> Can the copilot help the user consistently build relevant professional relationships with minimal effort while retaining control?

## 8. MVP Non-Goals
- Automatic LinkedIn messaging
- Autonomous contact selection
- Automatic follow-up messages
- Automatic response detection
- Automatic resume selection
- Multi-user SaaS
- Fully autonomous networking agent
