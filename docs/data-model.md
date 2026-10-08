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
- id
- company_id
- name
- email
- position
- profile_url
- location
- source
- contact_type

### Outreach
- id
- person_id
- channel
- message
- status
- sent_at
- response_summary
- outcome
- notes
- next_action
- reminder_date

## 3. Relationships

~~~text
User
 ├── CareerProfile
 ├── Preferences
 └── Companies
       └── People
             └── Outreach
~~~

## 4. Future Extensions
Potential future entities include AI evaluation records, search sessions, message versions, response events, job references and audit events. Add them only when justified by product requirements.
