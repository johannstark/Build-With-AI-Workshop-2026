# Role and Core Objective

You are an expert Cloud & AI Engineer. Your task is to scaffold a production-ready, serverless AI Agent designed to ingest and query internal company documentation (PTOs, expense policies, culture) from scratch.

The entire stack must be 100% serverless, fast, and optimized for Google Cloud deployment.

---

# Tech Stack Architecture

Generate the codebase strictly adhering to this architecture:

1. **Orchestrator:** Google Cloud ADK (Agent Development Kit) to manage the agent's thought loop and workflow.
2. **Data & Tooling Bridge:** MCP (Model Context Protocol) server to securely expose internal business functions (PTO lookup, expense registry).
3. **State & Memory:** Google Cloud Firestore to store and retrieve session-based chat history.
4. **Compute:** Google Cloud Run (Dockerized Python application) configured to scale to zero.

---

# Component Specifications

## 1. MCP Server (`mcp_server.py`)

Expose a Model Context Protocol server with the following tools:

* `get_pto_policy(employee_id: str) -> str`: Mocked response simulating a database lookup. Returns that the employee has 15 days of PTO and requires a 2-week notice.
* `submit_expense_claim(amount: float, category: str) -> str`: Simulates an expense registry. Returns a pre-approval status if the category is 'travel' or 'meals'.

## 2. AI Agent Core (`agent.py`)

Initialize the ADK Agent with:

* **System Instructions:** "Eres el asistente virtual de la empresa. Tu objetivo es resolver dudas sobre políticas internas, días libres (PTO) y gastos de forma clara y corporativa."
* **Tools:** Bind the tools exposed by the MCP server.
* **Memory Integration:** Connect `adk.FirestoreMemory` targeting a collection named `bogota-event-chats` to persist context across interactions.

## 3. Web Layer & Entrypoint (`main.py`)

* Create a simple FastAPI or Flask wrapper to expose a POST endpoint `/chat` that accepts `session_id`, `employee_id`, and `message`.
* The endpoint invokes the ADK Agent and returns the streaming or text response.

## 4. Deployment Assets

* `Dockerfile`: Multi-stage build optimized for Python, exposing port 8080 (Cloud Run standard).
* `requirements.txt`: Include `google-cloud-adk`, `mcp`, `google-cloud-firestore`, and the web framework choice.

---

# Code Generation Rules

* Write clean, well-documented Python code.
* Implement proper environment variable handling for Google Cloud Project IDs.
* Ensure the code is self-contained so it can be deployed to Cloud Run immediately via `gcloud run deploy`.
