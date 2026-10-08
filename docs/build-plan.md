# Career Networking Copilot — Build Plan

## Build Philosophy
The product will be implemented phase by phase. Claude Code receives the full project context but receives implementation instructions for only one phase at a time.

Each phase must be tested and documented before the next phase begins.

## Phase 1 — Preferences
Scope:
- Career profile
- Resume/profile
- Experience
- Skills
- Career positioning
- Networking preferences
- Daily outreach limit
- Persistence
- Edit/update

Explicitly excluded:
- Web search
- Company discovery
- AI recommendations
- Outreach generation
- Email
- LinkedIn

Completion criteria:
- Preferences can be entered.
- Preferences persist.
- Preferences can be edited.
- Data survives application restart.
- Daily outreach limit validates correctly.
- Tests pass.

## Phase 2 — Company Discovery
Preferences → Discovery → Web Search → Relevance Validation → Store → Display

Capabilities:
- Search companies using preferences
- Validate preferred-location presence
- Capture sources
- Store discovered companies
- Present company list

No automatic company ranking in MVP.

## Phase 3 — People / Contacts
This phase explicitly implements the continuous People → Contact workflow.

### AI recommendation path
Company → AI recommends person → User accepts → Contact record automatically created/pre-populated → User reviews/edits

Known fields should be carried forward automatically:
- Full name
- Company
- Position
- Location
- Profile URL
- Contact type
- Source
- Email, if available

### User research path
Company → User adds person → Contact record created → User reviews/edits

### Acceptance criteria
- Accepting an AI recommendation creates a structured contact record.
- Known information is pre-populated.
- User can correct or complete missing information.
- No duplicate re-entry is required.
- Contact source/provenance is retained.
- The contact record exposes **Draft Outreach**.

## Phase 4 — Outreach Generation
This phase begins from the Contact record, not from a disconnected message form.

### Workflow
Contact Record → Draft Outreach → Context Retrieval → LLM → Validation → User Review/Edit

### Context retrieved automatically
- Career profile
- Networking preferences
- Company information
- Person/contact information
- Relevant job information, if available
- Writing preferences
- Relevant previous outreach/interactions, if any

### Channel behavior
- LinkedIn: ask for character limit before generation and validate the result.
- Email: no mandatory character limit.

### Acceptance criteria
- Draft Outreach is available from a contact.
- The system retrieves the required context automatically.
- User does not re-enter known company/person information.
- Generated message is displayed immediately for review.
- User can edit or regenerate.
- LinkedIn character limit is respected.
- Relevant previous outreach is included when available.

## Phase 5 — Human Approval
Drafted → User Review/Edit → Approved → Execute

External outreach requires explicit approval.

The approval flow must preserve the connection to the Contact and Outreach record.

## Phase 6 — Outreach Tracking
Record status, channel, date, response summary, outcome, notes and next action. Status remains user-driven in MVP.

The resulting outreach record remains associated with the Contact.

## Phase 7 — Daily Limits & Reminders
- Enforce configurable daily outreach limit.
- Defer remaining opportunities.
- Remind user about non-response.
- Do not automatically send follow-ups.

## Phase 8 — AI Evaluation
Capture:
- AI recommendation
- Recommendation acceptance/rejection
- Contact fields automatically populated
- User corrections
- Message generation
- Message edits/rejection
- Human approval
- Final outcome

Establish baseline AI quality and workflow efficiency metrics.

## Claude Code Operating Model
For every phase:
1. Read all project context files.
2. Read the PRD and relevant architecture/data requirements.
3. Implement only the specified phase.
4. Do not silently expand scope.
5. Run relevant tests.
6. Review implementation against acceptance criteria.
7. Update implementation-status.md.
8. Report implementation, tests, decisions and known issues.
9. Stop.

## Standard Phase Prompt Structure
~~~text
CONTEXT
Read the project documentation first.

TASK
Implement Phase X.

SCOPE
Only the functionality specified for this phase.

CONSTRAINTS
Do not implement future phases.

ACCEPTANCE CRITERIA
Validate every criterion.

TESTING
Run relevant tests.

COMPLETION
Update implementation-status.md.
Report implementation, tests, decisions and known issues.
STOP.
~~~
