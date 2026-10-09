# Phase 1 Specification — Preferences

## Status
Phase 1 is approved for implementation following PRD sign-off. Implement only this phase.

## Objective
Build a usable, single-user Preferences area that captures and persistently stores the user's career profile and networking preferences. Later phases will use this data for company discovery and outreach, but those capabilities are out of scope here.

## Read first
- `docs/product-context.md`
- `docs/prd.md` — especially FR1 / US-01
- `docs/architecture.md`
- `docs/data-model.md`
- `docs/build-plan.md`

If documentation conflicts, do not silently resolve a product-level ambiguity. Report the conflict and choose the smallest safe implementation only when necessary to proceed.

## In scope

### A. Career profile
- Resume/profile content (allow pasted text; file upload is not required for Phase 1 unless already supported by the agreed architecture).
- Experience.
- Skills.
- Career positioning / target professional summary.

### B. Networking preferences
- Industry.
- Domain.
- Company types.
- Preferred locations.
- Target roles.

Use inputs suitable for multiple values where appropriate. The user must be able to enter, view, edit and save these values without repeatedly re-entering the whole profile.

### C. Writing and relationship preferences
- Writing preferences (for example tone, style, length or other user-defined guidance).
- Reusable message templates, including template name, channel/purpose where supported by the data model, and template body.
- Relationship-context defaults (for example new contact, known person, former colleague/collaborator, or custom). Do not assume any relationship as fact.

### D. Daily outreach limit
- A configurable, positive whole-number daily outreach limit.
- Validate the value and show a clear, actionable error for invalid input.
- Do not implement outreach counting, blocking, scheduling or reminders in Phase 1; those belong to later phases.

### E. Persistence and editing
- Save the single user's profile/preferences to the project's configured persistent store.
- Load saved values when the app opens or restarts.
- Support editing and updating the existing record without creating duplicate profiles/preferences.
- Show clear loading, save-success and save-error states as appropriate.
- Never display a success state when persistence failed.

## UX expectations
- Provide a clear Preferences page with logical sections: Career Profile, Networking Preferences, Writing & Templates, Relationship Context, and Daily Outreach Limit.
- Clearly distinguish required and optional fields. Follow the PRD: required fields must be identified and validated; optional fields may remain blank.
- Preserve user-entered content when validation fails.
- Make the saved state understandable and accessible; use labels and text errors, not color alone.
- Keep the UI simple and consistent with the existing project. Do not add unrelated screens or polish that delays acceptance criteria.

## Data and implementation rules
- Follow the existing architecture and data model; inspect the current repository before choosing libraries or changing structure.
- The persistent database is the source of truth. Do not keep preferences only in component state or browser memory.
- Keep secrets and API keys out of source control and client-side code.
- Do not add an LLM, web-search integration, or external messaging integration in this phase.
- Do not add dependencies unless necessary; explain any new dependency.
- Do not introduce a multi-user/authentication system; this is a single-user personal MVP.
- Do not implement features from later phases, even if they seem convenient.

## Acceptance criteria
1. The Preferences page exposes all in-scope fields listed above.
2. A user can save valid values and receives a clear confirmation only after the persistent write succeeds.
3. On refresh/restart, previously saved values are loaded from persistent storage.
4. A user can edit existing values and save; updates do not create duplicate profile/preferences records.
5. Multi-value fields support entering and editing more than one value where appropriate.
6. Invalid or missing required values are clearly identified; optional fields remain optional.
7. Daily outreach limit rejects blank, non-numeric, non-integer, zero and negative values, and does not persist invalid input.
8. Failed saves show a useful error and retain the user's unsaved form input.
9. Automated tests cover validation, create/update persistence, loading saved data, and the daily outreach limit.
10. Existing project tests/build continue to pass; no later-phase functionality is introduced.

## Explicitly out of scope
- Web search or company discovery.
- Company records, company disposition or ranking.
- AI people recommendations or contact management.
- LLM integration or AI-generated content.
- Outreach generation, approval, sending or tracking.
- Email or LinkedIn integrations.
- Daily outreach enforcement/counting, reminders or follow-ups.
- AI evaluation/observability features.
- Authentication or multi-user support.

## Required completion report
After implementation:
1. Run relevant automated tests and the project's build/lint checks if configured.
2. Map each acceptance criterion to evidence (test, behavior checked, or clearly state not verified).
3. Update `docs/implementation-status.md` with Phase 1 status, files changed, tests run/results, decisions, and known issues.
4. If a requirement cannot be implemented without changing agreed architecture or scope, stop and report the blocker rather than silently expanding scope.
5. Stop after Phase 1. Do not begin Phase 2.
