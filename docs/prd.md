# Career Networking Copilot — Product Requirements Document

## 1. Product Objective
Build an AI-powered copilot that helps professionals proactively discover relevant companies, identify potential contacts, create personalized outreach, and track networking activity.

**Core principle:** AI discovers and prepares. The user decides and acts.

## 2. Target User
The primary user is an individual professional seeking to build a career network proactively. The MVP is single-user.

## 3. MVP User Journey
Preferences → Discover Companies → Review Companies → Identify/Add Person → Contact Record → Draft Outreach → Review/Edit → Human Approval → Outreach → Track

## 4. Functional Requirements

### FR1 — Career & Networking Preferences
The user can configure career profile, resume/profile, experience, skills, career positioning, industry, domain, company type, preferred locations, target roles, writing preferences and daily outreach limit. Preferences are persisted for future discovery and personalization.

### FR2 — Company Discovery
The system discovers companies based on user preferences. Capture company name, website, industry/domain, company type, presence in preferred location(s), relevant information, open jobs if available, and source. Open jobs are informational, not a prerequisite. The MVP presents discovered companies and does not automatically rank them.

### FR3 — People Identification
The People experience begins from a selected company and supports two paths:

1. **AI recommendation:** The system recommends potential contacts such as HR/Talent Acquisition, relevant Product leaders, or people in closely related roles.
2. **User research:** The user can add a person they found independently.

Location relevance can influence AI recommendations but is not a mandatory filter.

When the user accepts an AI recommendation, the system must automatically create a contact record and pre-populate every available field from the recommendation/search result, including:
- Full name
- Company
- Position
- Location
- Profile URL
- Contact type
- Source
- Email, if available
- Any other relevant discovered information

The user then reviews the record and only fills in or corrects missing/incorrect information.

**The AI recommendation must become structured product data and remain available to downstream workflow steps. It should not be displayed and discarded.**

### FR4 — Contact Management
Contact Management is the structured handoff between People Identification and Outreach.

A contact record is created automatically when an AI recommendation is accepted, or when the user adds a person independently.

The record stores:
- Full name
- Email
- Position
- Company
- Role / Job ID, if applicable
- Profile URL
- Location
- Contact type
- Source
- Tailored resume, if selected later
- Outreach status
- Last contacted date
- Next reminder
- Message history
- Outcome
- Notes

The contact record should expose a clear **Draft Outreach** action.

The user should not re-enter information already available in the contact record.

### FR5 — Personalized Outreach
Once a contact record exists, the user can select **Draft Outreach**.

The system automatically retrieves relevant context:
- Career profile
- Networking preferences
- Company information
- Person/contact information
- Relevant job information, if available
- Writing preferences
- Relevant previous interaction/outreach, if any

The context builder passes only the relevant information to the LLM.

The workflow is:

**Contact Record → Draft Outreach → Context Retrieval → AI Message Generation → User Review/Edit**

For LinkedIn:
- Ask for the required character limit before generating the message.
- Validate that the generated message stays within the user-provided limit.

For Email:
- No mandatory character limit.
- The user may specify desired length or tone through writing preferences or the drafting experience.

The generated message should be immediately available for user review and editing.

### FR6 — Human Approval
External outreach follows:

**AI Draft → User Review/Edit → User Approval → Outreach**

No external message is sent without user approval.

For LinkedIn MVP, the system prepares the message and the user performs the LinkedIn action.

### FR7 — Daily Outreach Limit
The user configures a daily outreach limit. When reached, do not suggest additional outreach for that day; carry remaining opportunities forward; allow the user to change the limit.

### FR8 — Outreach Tracking
Suggested statuses:
Not Contacted → Drafted → Approved → Sent → Responded → No Response → Interested → Not Interested → Closed

The user can record date, channel, response summary, notes, next action, reminder and outcome. AI must not assume an external action or response occurred.

### FR9 — Follow-up Reminder
The system can remind the user when a contact has not responded. It does not automatically send follow-ups. The user decides whether to follow up, find another contact, or close the opportunity.

### FR10 — AI Correctability
For AI-generated classification or prioritization, the user can accept the AI decision, change classification, change priority, and optionally provide a correction reason. Record the original AI decision and final human decision as an evaluation signal.

## 5. End-to-End Workflow Requirement

FR3, FR4 and FR5 are one continuous workflow, not disconnected forms.

### AI-recommended contact
**AI recommends person → User accepts → Contact record automatically created/pre-populated → User reviews/edits → Draft Outreach → AI retrieves context → Message generated → User reviews/edits → Human approval → Outreach**

### User-researched contact
**User adds person → Contact record created → Draft Outreach → AI retrieves context → Message generated → User reviews/edits → Human approval → Outreach**

### UX rule
**Never ask the user to re-enter information that the system already knows.**

## 6. Non-Functional Requirements
- **Privacy:** Store career profile and outreach information securely.
- **Explainability:** Where practical, show why a company or person was considered relevant.
- **Traceability:** AI-generated decisions, source information and human corrections should be auditable.
- **Reliability:** Consequential external actions require explicit user approval.
- **Context efficiency:** The LLM receives relevant retrieved context rather than the entire database.
- **Data continuity:** Information discovered in one workflow step must be persisted and available to downstream steps.

## 7. Success Metrics

### User / Business Outcome
- Relevant companies discovered
- Relevant contacts identified
- Contact records created without duplicate data entry
- Outreach drafted
- Outreach sent
- Response rate
- Interested-contact rate

### AI Quality
- Messages accepted without edits
- Messages edited
- Messages rejected
- AI decisions corrected
- Percentage of accepted AI recommendations successfully converted into usable contact records

### Productivity
- Time saved per outreach
- Outreach consistency
- Daily limit adherence
- Reduction in manual data re-entry

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
