# Career Networking Copilot — Data Model

## 1. Design Principle
The database is the persistent source of truth for structured business data. LLM context is retrieved at runtime and is not a replacement for the database.

## 2. Core Entities

### User
- id
- name
- email
- created_at

### CareerProfile
- id
- user_id
- resume
- experience
- skills
- career_positioning

### Preferences
- id
- user_id
- industry
- domain
- company_types
- preferred_locations
- target_roles
- writing_preferences
- daily_outreach_limit

### Company
- id
- name
- website
- industry
- domain
- company_type
- locations
- relevant_information
- source_url
- discovered_at

### Person
Represents the information discovered or entered about a potential contact before and during contact creation.

- id
- company_id
- name
- email
- position
- profile_url
- location
- source
- contact_type

### Contact
The persistent, user-reviewed contact record created when an AI recommendation is accepted or when the user adds a person independently.

- id
- person_id
- company_id
- name
- email
- position
- location
- profile_url
- contact_type
- source
- role_or_job_id
- tailored_resume
- notes
- created_at
- updated_at

The Contact record is the downstream handoff between People Identification and Outreach.

Known information from an AI recommendation/search result should populate this record automatically. User edits should update the structured record rather than requiring duplicate entry.

### Outreach
Represents an outreach attempt or draft associated with a contact.

- id
- contact_id
- channel
- message
- status
- sent_at
- response_summary
- outcome
- notes
- next_action
- reminder_date

### Message Context
Optional implementation-level record for the context used to generate a message.

- id
- outreach_id
- company_context
- person_context
- job_context
- profile_context
- preference_context
- previous_outreach_context
- created_at

This can be implemented later if full context traceability is needed.

## 3. Relationships

~~~text
User
 ├── CareerProfile
 ├── Preferences
 └── Companies
       └── People
             ↓
          Contacts
             ↓
          Outreach
             ↓
        Message Context
~~~

## 4. Data Continuity Rule

Information should flow forward through the product:

**Discovery data → Person recommendation → Contact record → Outreach context → Message → Outcome**

The same information should not be requested again unless it is missing, stale or requires user correction.

## 5. Future Extensions
Potential future entities include AI evaluation records, search sessions, message versions, response events, job references and audit events. Add them only when justified by product requirements.
