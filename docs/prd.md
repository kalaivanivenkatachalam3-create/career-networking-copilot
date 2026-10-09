# Career Networking Copilot — Product Requirements Document

## 1. Product Summary

Career Networking Copilot helps professionals proactively discover relevant companies, identify potential contacts, create personalized outreach, and track networking activity—even when no suitable job is currently advertised.

**Product principle:** AI discovers and prepares; the user decides and acts.

## 2. Target User and MVP Boundaries

- **Primary user:** An individual professional building a career network proactively.
- **MVP model:** Single-user personal tool.
- **Channels:** Email and LinkedIn message preparation.
- **External action:** The user remains in control. LinkedIn messages are manually sent by the user; no external message may be sent without explicit approval.
- **MVP implementation:** Phase-by-phase build. Each phase must meet its acceptance criteria before the next begins.

## 3. MVP Journey

Preferences → Discover Companies → Review Companies → Identify/Add Person → Contact Record → Draft Outreach → Review/Edit → Human Approval → User Executes Outreach → Track Outcome

AI-recommended contacts and independently researched contacts converge into the same Contact record and Draft Outreach workflow.

## 4. Functional Requirements, User Stories and Acceptance Criteria

### FR1 — Career and Networking Preferences

**Requirement:** The user can configure and maintain career profile and networking preferences.

**User story US-01:** As a professional, I want to save my career profile and networking preferences so that company discovery and outreach can be personalized without repeatedly entering the same information.

**Acceptance criteria**
1. Given the user opens Preferences, when the form is displayed, then it supports career profile/resume, experience, skills, career positioning, industry, domain, company types, preferred locations, target roles, writing preferences and daily outreach limit.
2. Given the user enters valid values and saves, when the save completes, then the values are persisted and a saved state is shown.
3. Given saved preferences exist, when the user returns or restarts the app, then the saved values are loaded.
4. Given the user edits a preference, when the user saves, then the updated value replaces the prior value without creating a duplicate profile.
5. Given an invalid daily outreach limit, when the user saves, then the app explains the validation error and does not persist the invalid value.
6. Given required fields are missing, when the user saves, then the UI clearly identifies what must be completed. Optional fields remain optional.

### FR2 — Company Discovery

**Requirement:** Discover companies based on saved preferences and show source-backed information without automatically ranking companies in the MVP.

**User story US-02:** As a professional, I want to discover companies that fit my target domain and locations so that I can build a network even when no suitable job is open.

**Acceptance criteria**
1. Given valid preferences exist, when the user starts discovery, then the system uses the saved industry, domain, company type and location preferences as search inputs.
2. Given search results are returned, then each company result displays the company name and, when available, website, industry/domain, company type, presence in preferred location(s), relevant information, open jobs and source URL.
3. Given a company has multiple offices, when its result is displayed, then presence in the user's preferred location(s) is shown where supported by evidence; a large global footprint alone is not treated as proof of local presence.
4. Given open jobs are not found, then the company can still be shown as a networking target.
5. Given results are displayed, then the MVP does not assign an automatic company ranking or score.
6. Given search fails or returns no usable results, then the UI communicates this clearly and offers retry/edit-search options without fabricating companies.
7. Given a company is selected, then its stored record is available to downstream People and Contact workflows.
8. Company claims should retain source URLs where available; unavailable information is shown as unknown rather than invented.

### FR3 — People Identification

**Requirement:** From a selected company, the system can recommend potential contacts, while allowing the user to add independently researched people.

**User story US-03A:** As a professional, I want AI to suggest relevant people at a target company so that I can identify a useful person to approach.

**Acceptance criteria**
1. Given a company is selected, when the user requests people recommendations, then the system may suggest HR/Talent Acquisition, a relevant Product leader, or a person in a closely related role.
2. Each recommendation displays available name, position, location, profile URL, contact type, company and source.
3. Location relevance may inform recommendations but is not a mandatory filter.
4. The UI distinguishes verified/available information from missing information; it does not invent contact details.
5. The user can accept or dismiss a recommendation. No contact is created merely because a recommendation was displayed.
6. When a recommendation is accepted, the system creates a structured Contact record and carries forward all available information (see FR4).
7. If recommendation/search fails, the user can retry or use the independent-add path.

**User story US-03B:** As a professional, I want to add a person I found through my own research so that I can use the same outreach workflow even if AI did not recommend them.

**Acceptance criteria**
1. The user can start Add Person from a selected company.
2. The form uses the selected company automatically and does not require the user to re-enter it.
3. The user can enter available person details and a source/profile URL.
4. The app validates required fields and clearly identifies missing information.
5. Saving creates a Contact record associated with the selected company.
6. After saving, the user reaches the same Contact review and Draft Outreach workflow used for AI-recommended contacts.

### FR4 — Contact Management and Data Continuity

**Requirement:** An accepted AI recommendation or user-added person becomes a persistent, editable Contact record. The contact record is the handoff between People Identification and Outreach.

**User story US-04A:** As a professional, I want accepted AI recommendations to pre-populate a contact record so that I do not re-enter information the system already knows.

**Acceptance criteria**
1. Given an AI recommendation contains person information, when the user accepts it, then a Contact record is created automatically.
2. The record is pre-populated with every available relevant field, including full name, company, position, location, profile URL, contact type, source and email if available.
3. Information from the selected company is carried into the contact record automatically.
4. Missing fields remain clearly marked as missing; the system does not fabricate values.
5. The user can review, edit or complete the record before drafting outreach.
6. User corrections persist and are used by subsequent outreach generation.
7. The record retains source/provenance for discovered information where available.

**User story US-04B:** As a professional, I want to maintain a single contact record with outreach history so that future messages can use relevant context.

**Acceptance criteria**
1. The Contact record supports name, email, position, company, role/job reference if applicable, profile URL, location, contact type, source, notes and relevant resume reference if selected later.
2. The Contact record exposes a clear **Draft Outreach** action.
3. Outreach attempts/messages are associated with the correct Contact.
4. Existing contact and company details are reused in downstream workflows rather than requested again.
5. The UI avoids duplicate contact creation when an existing contact can be identified with reasonable confidence; if a possible duplicate is found, the user can review it before creating another record.
6. A contact can exist even if email or other optional fields are unavailable.

### FR5 — Personalized Outreach

**Requirement:** Selecting Draft Outreach from a Contact retrieves relevant context and generates a message for immediate review/editing.

**User story US-05:** As a professional, I want a personalized message drafted from my profile and the selected contact's context so that I can reach out with less manual effort.

**Acceptance criteria**
1. Given a Contact record exists, when the user selects **Draft Outreach**, then the user chooses or confirms Email or LinkedIn.
2. Before generation, the system retrieves relevant context from the career profile, networking preferences, company, contact/person, relevant job information if available, writing preferences and relevant previous outreach/interactions if any.
3. The system passes only relevant context to the LLM; it does not send the entire database by default.
4. The generated message uses available evidence and does not invent a relationship, experience, job opening or personal detail.
5. The generated message is linked to the correct Contact and channel.
6. The message is displayed immediately for user review and editing.
7. The user can edit or regenerate the message. Regeneration does not silently overwrite a user-edited message without confirmation.
8. If required context is missing, the system either generates a cautious draft using available information or asks for the specific missing input; it does not invent facts.
9. Previous outreach is included only when relevant and available.

**LinkedIn-specific criteria**
10. Before generating a LinkedIn message, the UI asks for the user's character limit (or confirms a configured limit).
11. The generated message is validated against that limit, including spaces and punctuation.
12. If the draft exceeds the limit, the system shortens/regenerates it or clearly prompts the user to revise; it must not mark an over-limit draft as valid.

**Email-specific criteria**
13. Email has no mandatory character limit.
14. The user may specify a desired length or tone; otherwise saved writing preferences are used.

### FR6 — Human Review and Approval

**Requirement:** The user reviews and approves outreach before taking the external action.

**User story US-06:** As a professional, I want to inspect and approve every outreach message so that no message is sent on my behalf without my consent.

**Acceptance criteria**
1. A generated message starts in Drafted state and is not treated as sent.
2. The user can edit the draft before approval.
3. Approval is an explicit action separate from editing or saving.
4. The app records approval state and time where appropriate.
5. For LinkedIn in the MVP, the user copies/uses the approved draft and sends it manually on LinkedIn; the product does not automate LinkedIn sending.
6. No external action is performed without explicit user approval.
7. If the user rejects a draft, it remains unsent and can be edited, regenerated or discarded.

### FR7 — Daily Outreach Limit

**Requirement:** The user controls daily outreach volume to support consistency without pressure.

**User story US-07:** As a professional, I want a configurable daily outreach limit so that networking remains manageable.

**Acceptance criteria**
1. The user can set and later change a daily limit.
2. The app shows how many outreach actions have counted toward the current day's limit.
3. Once the limit is reached, the app does not recommend additional outreach actions for that day.
4. Remaining opportunities remain saved and can be revisited on a later day.
5. Reaching the limit does not trigger automatic sending or follow-up.
6. The UI communicates the limit neutrally and without guilt-inducing language.

### FR8 — Outreach Tracking

**Requirement:** The user manually records outreach status and outcomes.

**User story US-08:** As a professional, I want to track the status and outcome of each contact interaction so that I can manage relationships over time.

**Acceptance criteria**
1. The user can record channel, date, status, response summary, notes, next action, reminder and outcome.
2. Suggested statuses are Not Contacted, Drafted, Approved, Sent, Responded, No Response, Interested, Not Interested and Closed.
3. Status changes are user-driven in the MVP; the system does not infer that a message was sent or a response received.
4. Each outreach record remains associated with its Contact and message history.
5. The user can view prior outreach before drafting a new message.
6. Invalid status changes are prevented or clearly explained where workflow rules apply.

### FR9 — Follow-up Reminders

**Requirement:** Remind the user about non-response without automatically sending follow-ups.

**User story US-09:** As a professional, I want a reminder when a contact has not responded so that I can decide what to do next.

**Acceptance criteria**
1. The user can set or update a reminder date/next action.
2. A due reminder is surfaced in the app.
3. The reminder shows the related contact and relevant outreach history.
4. The user can choose to follow up, find another contact, reschedule or close the opportunity.
5. The system never automatically sends a follow-up message in the MVP.

### FR10 — AI Correctability and Feedback

**Requirement:** User corrections to AI recommendations/classifications are captured as feedback.

**User story US-10:** As a user, I want to correct AI recommendations so that the final record reflects my judgment and AI quality can be evaluated.

**Acceptance criteria**
1. Where AI provides a classification or recommendation that supports correction, the UI allows the user to accept or correct it.
2. The system retains the original AI output and the user's final decision.
3. The user can optionally provide a reason for the correction.
4. A correction updates the product record used by downstream steps.
5. Corrections are available for evaluation; they do not silently retrain or change the model in the MVP.

## 5. Cross-Feature Workflow and Acceptance Criteria

FR3, FR4 and FR5 are one continuous workflow, not disconnected forms.

### AI-recommended contact path
AI recommends person → User accepts → Contact automatically created/pre-populated → User reviews/edits → Draft Outreach → Context retrieval → Message generated → User reviews/edits → Human approval → User executes outreach.

### User-researched contact path
User adds person → Contact record created → User reviews/edits → Draft Outreach → Context retrieval → Message generated → User reviews/edits → Human approval → User executes outreach.

**End-to-end acceptance criteria**
1. An accepted AI recommendation creates one persisted Contact record with all available known fields carried forward.
2. A user-added contact enters the same downstream workflow.
3. In both paths, Draft Outreach is available from the Contact record.
4. Draft Outreach retrieves the same categories of relevant context for either path.
5. The user does not re-enter company/person information already stored.
6. The resulting message is associated with the correct Contact, channel and outreach record.
7. The user can review/edit before approval; no external action happens without explicit approval.
8. A failed search or incomplete person record does not block manual correction or falsely populate unknown fields.

## 6. Non-Functional Requirements

- **Privacy:** Store career profile and outreach information securely; do not expose secrets in source control.
- **Explainability:** Where practical, show why a company or person was considered relevant.
- **Traceability:** AI outputs, source information and human corrections should be auditable.
- **Reliability:** Consequential external actions require explicit user approval.
- **Context efficiency:** The LLM receives relevant retrieved context rather than the entire database.
- **Data continuity:** Information discovered in one workflow step is persisted and available to downstream steps.
- **Error handling:** Search/API/LLM failures are shown clearly; do not fabricate success or data.
- **Usability:** Preserve user-entered edits and clearly distinguish Drafted, Approved and Sent states.

## 7. Success Metrics

### User / Business Outcome
- Relevant companies discovered
- Relevant contacts identified
- Contact records created without duplicate data entry
- Outreach drafted and sent
- Response rate
- Interested-contact rate

### AI Quality
- Messages accepted without edits
- Message edit/rejection rate
- AI decisions corrected
- Percentage of accepted AI recommendations successfully converted into usable contact records
- Contact auto-population completeness

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

## 9. Dependencies and Open Implementation Decisions

The product requirements do not yet mandate a specific web search provider, LLM provider, email-sending integration or production hosting provider. These are technical decisions to be confirmed during implementation.

- Phase 2 depends on saved Preferences.
- Phase 3 depends on persisted Company records.
- Phase 4 depends on Contact records and context retrieval.
- Phase 5 depends on generated messages and explicit approval state.
- Phase 6 depends on persistent Contact and Outreach records.
- Phase 7 depends on dates/statuses in Outreach.
- Phase 8 depends on capturing AI outputs and human feedback.
