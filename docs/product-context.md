# Career Networking Copilot — Product Context

## Product Vision
Help professionals build meaningful relationships with target companies proactively, rather than depending only on published job openings.

## Product Philosophy
**AI discovers and informs; the user decides and acts.**

## Primary User
An individual professional seeking to build a career network proactively. The MVP is personal and single-user.

## Core MVP Loop
Preferences → Discover Companies → Review → Identify/Add People → Contact Record → Draft Outreach → Human Review/Approval → Outreach → Track

## Core Product Principles
1. AI can discover, analyze, recommend and prepare.
2. An AI recommendation becomes structured product data when accepted; it is not merely displayed and discarded.
3. The user remains the decision-maker for people selection and external actions.
4. The system should not ask the user to re-enter information it already knows.
5. Human approval is required before consequential external outreach.
6. AI classification and prioritization must be correctable by the user.
7. Persistent business data belongs in a structured database, not general AI memory.
8. Retrieve only relevant context for each AI task.
9. Automate progressively as confidence and evidence increase.
10. Networking should support consistent progress without pressure or guilt.

## Important Product Decisions

### Company discovery
- Discover companies using user preferences and web search.
- Validate presence in preferred locations.
- Present the discovered company list.
- Do not automatically rank companies in the MVP.
- Open jobs are informative, not required for networking.
- Use web search as discovery evidence, preserve source URLs/retrieval dates, prefer credible/official sources, and label uncertain facts rather than inventing them.
- Track company disposition separately from individual outreach status: Not Reviewed, In Scope, Out of Scope, Networking Planned, Outreach in Progress, Outreach Done, Revisit Later.
- When marked Out of Scope, capture a reason such as capability/domain, role/experience, location, or other mismatch.

### People
- AI may recommend HR/Talent Acquisition and role-relevant contacts based on the user's target roles: e.g. Product leaders for Product roles, Engineering leaders/directors for Engineering roles, and Project/Program Managers for project/program roles.
- Location relevance is a recommendation signal, not a hard filter.
- The user can accept an AI recommendation or add a person found independently.
- When an AI recommendation is accepted, available information is automatically carried into the contact record.
- User-entered information should supplement or correct missing information rather than duplicate known information.

### Contact-to-outreach workflow
The People, Contact and Outreach experiences are one continuous workflow:

AI recommends person → User accepts → Contact record is automatically created/pre-populated → User reviews/edits → User clicks Draft Outreach → AI retrieves relevant context → Message generated → User reviews/edits → Human approval → Outreach

For user-researched contacts:

User adds person → Contact record → Draft Outreach → AI-generated message → Review → Approval

### Outreach
- Support Email and LinkedIn.
- User can configure reusable message templates and choose a template per outreach.
- Drafting adapts to relationship context (new contact, known person, former colleague/collaborator, or user-defined context); prior relationship is never assumed.
- User may attach a job link/title/ID when they have applied or want to discuss a specific role.
- AI drafts personalized messages from the selected contact record and retrieved context.
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
Observe → Understand → Decide → Prepare → Validate → Human Review → Human Approval → Execute → Record Outcome → Learn from Feedback

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
