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
Two paths:
1. AI contact recommendations → User selects
2. User research → User adds person

Store contact information and source.

## Phase 4 — Outreach Generation
Profile + Preferences + Company + Person + Relevant History → Context Builder → LLM → Message → Validation

Support Email and LinkedIn drafts. LinkedIn character limit is user-provided.

## Phase 5 — Human Approval
Drafted → User Review → Edit/Regenerate → Approved → Execute

External outreach requires explicit approval.

## Phase 6 — Outreach Tracking
Record status, channel, date, response summary, outcome, notes and next action. Status remains user-driven in MVP.

## Phase 7 — Daily Limits & Reminders
- Enforce configurable daily outreach limit.
- Defer remaining opportunities.
- Remind user about non-response.
- Do not automatically send follow-ups.

## Phase 8 — AI Evaluation
Capture AI output, user acceptance, user edits, rejection, human correction and final outcome. Establish baseline AI quality metrics.

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
