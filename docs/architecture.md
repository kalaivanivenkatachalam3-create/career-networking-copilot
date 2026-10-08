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
  ├── Context Retrieval
  ├── Outreach Generation
  ├── Validation
  └── Tracking
  ↓
Database / Web Search / LLM API
  ↓
Human Approval
  ↓
External Channel
~~~

## 2. Architecture Responsibilities

### User Interface
Preferences, company discovery, contact management, message review, approval, status tracking, reminders and AI corrections.

### Copilot Orchestrator
Coordinates workflow state and invokes the required services. The orchestrator is not the LLM itself.

### LLM API
Intent understanding, reasoning, summarization, recommendations, message generation, classification and validation.

### Web Search Layer
Company discovery, location validation, company information, potential contact discovery and current job information. Search results should retain source URLs for traceability.

### Context Retrieval Layer
Retrieves only relevant data from the database for the current AI task.

### Database
Persistent source of truth for structured product data.

### Human Approval Layer
Required before consequential external outreach.

## 3. AI Workflow
Observe → Understand → Decide → Prepare → Validate → Human Approval → Execute → Record Outcome → Learn from Feedback

## 4. Human-in-the-Loop Controls

### AI Classification / Prioritization
AI decision → User accepts or corrects → Record correction → Evaluation signal

### External Action
AI prepares action → User approval required → Execute

## 5. Evaluation
Capture AI output, acceptance, user edits, rejection, human correction and final outcome.

Potential metrics:
- Message acceptance rate
- Edit rate
- Rejection rate
- Classification correction rate
- Response rate

## 6. Initial Technology Direction
- Frontend: HTML / CSS / JavaScript
- Backend: Node.js
- LLM: LLM API
- Search: Web search API
- Database: SQLite initially
- Orchestration: Custom lightweight orchestration logic

The architecture should remain modular so components can be replaced as the product evolves.

## 7. Framework Decision
LangChain/LangGraph are not required for the initial implementation. The project intentionally demonstrates lightweight orchestration fundamentals before introducing an agent framework.

Langfuse is an optional future addition for tracing, observability and evaluation.
