# Career Networking Copilot — Architecture

## 1. High-Level Architecture

~~~text
User
  ↓
Web Application
  ↓
Copilot Orchestrator
  ├── Company Discovery
  ├── People Research
  ├── Contact Record Service
  ├── Context Retrieval
  ├── Outreach Generation
  ├── Validation
  └── Tracking
  ↓
Database / Web Search / LLM API
  ↓
Human Review + Approval
  ↓
External Channel
~~~

## 2. Core Data Flow

The product is designed as a continuous data flow rather than disconnected screens.

~~~text
Company Discovery
      ↓
Selected Company
      ↓
People Recommendation / User Research
      ↓
Person Information
      ↓
Accept Recommendation / Add Person
      ↓
Contact Record Created + Pre-populated
      ↓
User Review / Correction
      ↓
Draft Outreach
      ↓
Context Retrieval
      ├── Career Profile
      ├── Networking Preferences
      ├── Company
      ├── Person
      ├── Relevant Job (if available)
      ├── Writing Preferences
      └── Previous Outreach (if any)
      ↓
LLM Message Generation
      ↓
Message Validation
      ↓
User Review / Edit
      ↓
Human Approval
      ↓
External Outreach
      ↓
Outcome / Status
      ↓
Database
~~~

## 3. Architecture Responsibilities

### User Interface
Provides:
- Preferences
- Company discovery
- People recommendations
- Add-person flow
- Contact record review/edit
- **Draft Outreach** action
- Message review/edit
- Approval
- Status tracking
- Reminders
- AI corrections

The UI should preserve continuity between screens. Accepting a recommendation should take the user into the populated contact record rather than requiring a second manual form.

### Copilot Orchestrator
Coordinates workflow state and invokes the required services.

The orchestrator is not the LLM itself.

It should pass structured outputs from one step to the next, especially the accepted person recommendation → contact record → outreach context flow.

### LLM API
Used for:
- Intent understanding
- Reasoning
- Summarization
- Contact recommendations
- Message generation
- Classification
- Validation

### Web Search Layer
Used for:
- Company discovery
- Location validation
- Company information
- Potential contact discovery
- Current job information

Search results should retain source URLs and available evidence for traceability.

### Contact Record Service
Converts accepted person information into structured product data.

Responsibilities:
- Create a contact record from AI recommendation data
- Pre-populate known fields
- Preserve source/provenance
- Allow user corrections
- Expose the contact to downstream outreach workflow

### Context Retrieval Layer
When the user selects **Draft Outreach**, retrieve only relevant information for that contact:
- Career profile
- Networking preferences
- Company
- Person
- Relevant job information, if available
- Writing preferences
- Previous outreach/interactions, if any

### Database
Persistent source of truth for structured product data.

### Human Review / Approval Layer
There are two review points:
1. **Contact review:** user reviews/corrects the populated contact record.
2. **Message review:** user reviews/edits the generated outreach message.

Human approval is required before consequential external outreach.

## 4. AI Workflow

Observe → Understand → Decide → Prepare Contact Data → Persist → User Review → Retrieve Context → Generate Message → Validate → User Review/Edit → Human Approval → Execute → Record Outcome → Learn from Feedback

## 5. Human-in-the-Loop Controls

### AI Recommendation
AI recommendation → User accepts → Structured contact record → User corrects if needed

### AI Classification / Prioritization
AI decision → User accepts or corrects → Record correction → Evaluation signal

### External Action
AI prepares action → User approval required → Execute

## 6. Evaluation

Capture:
- AI recommendation
- Source/provenance
- User acceptance/rejection
- Contact fields changed by user
- AI-generated message
- Message edits
- Message rejection
- Human approval
- Final outreach outcome

Potential metrics:
- Recommendation acceptance rate
- Contact auto-population completeness
- Contact correction rate
- Message acceptance rate
- Edit rate
- Rejection rate
- Classification correction rate
- Response rate

## 7. Initial Technology Direction
- Frontend: HTML / CSS / JavaScript
- Backend: Node.js
- LLM: LLM API
- Search: Web search API
- Database: SQLite initially
- Orchestration: Custom lightweight orchestration logic

The architecture should remain modular so components can be replaced as the product evolves.

## 8. Framework Decision
LangChain/LangGraph are not required for the initial implementation. The project intentionally demonstrates lightweight orchestration fundamentals before introducing an agent framework.

Langfuse is an optional future addition for tracing, observability and evaluation.
