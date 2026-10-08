# Career Networking Copilot — Product Context

## Product Vision
Help professionals build meaningful relationships with target companies proactively, rather than depending only on published job openings.

## Product Philosophy
**AI discovers and informs; the user decides and acts.**

## Primary User
An individual professional seeking to build a career network proactively. The MVP is personal and single-user.

## Core MVP Loop
Preferences → Discover Companies → Review → Identify/Add People → Draft Outreach → Human Approval → Outreach → Track

## Core Product Principles
1. AI can discover, analyze, recommend and prepare.
2. The user remains the decision-maker for people selection and external actions.
3. Human approval is required before consequential external outreach.
4. AI classification and prioritization must be correctable by the user.
5. Persistent business data belongs in a structured database, not general AI memory.
6. Retrieve only relevant context for each AI task.
7. Automate progressively as confidence and evidence increase.
8. Networking should support consistent progress without pressure or guilt.

## Important Product Decisions

### Company discovery
- Discover companies using user preferences and web search.
- Validate presence in preferred locations.
- Present the discovered company list.
- Do not automatically rank companies in the MVP.
- Open jobs are informative, not required for networking.

### People
- AI may recommend HR, Talent Acquisition, relevant Product leaders, or people in closely related roles.
- Location relevance is a recommendation signal, not a hard filter.
- The user selects an AI-recommended person or adds someone found independently.

### Outreach
- Support Email and LinkedIn.
- AI drafts personalized messages.
- LinkedIn character limits are supplied by the user before drafting.
- No automatic LinkedIn sending in MVP.
- External actions require human approval.

### Follow-up
- No automatic follow-up sequence in MVP.
- The system may remind the user about non-response.
- The user decides whether to follow up, find another contact, or close the opportunity.

### Daily outreach limit
- User-configurable.
- Prevent additional outreach suggestions after the daily limit is reached.
- Remaining opportunities can be carried forward.
- Purpose: consistent progress without pressure.

### Status
Suggested lifecycle:
Not Contacted → Drafted → Approved → Sent → Responded → No Response → Interested → Not Interested → Closed

Status is user-driven in the MVP.

## Data vs AI Context
The database is the source of truth for companies, people, contact details, outreach, messages, statuses, dates, outcomes, notes and reminders.

AI context should contain stable preferences and only the relevant records retrieved at runtime.

## AI Workflow
Observe → Understand → Decide → Prepare → Validate → Human Approval → Execute → Record Outcome → Learn from Feedback

## MVP Non-Goals
- Automatic LinkedIn messaging
- Autonomous contact selection
- Automatic follow-up messages
- Automatic response/status detection
- Automatic resume selection
- Multi-user support
- Fully autonomous networking agent

## Technology Direction
- Frontend: HTML/CSS/JavaScript
- Backend: Node.js
- LLM: LLM API
- Search: Web search API
- Database: SQLite initially
- Orchestration: Lightweight custom orchestration logic

LangChain/LangGraph are intentionally not required for the initial prototype. Langfuse may be considered later for observability/evaluation.
