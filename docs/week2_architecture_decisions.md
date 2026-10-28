# Architecture Decision Record (ADR) & Traceability Matrix

## Architecture Decision Record (ADR)

| Decision | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
| :--- | :--- | :--- | :--- | :--- |
| **ADR1: Grounding via Document Retrieval (RAG)** | FR1, FR3, RAI4 (Must cite official scholarship documents and avoid hallucinations) | 1. Fine-tuning a base LLM.<br>2. Direct zero-shot LLM prompts.<br>3. Document-grounded RAG component. | Document-grounded RAG pipeline | Higher system architecture complexity, but guarantees verifiable citations and up-to-date document accuracy. |
| **ADR2: Explicit Input Guardrail & Scope Control** | RAI2, FR4 (Must refuse out-of-scope legal/academic queries) | 1. System prompt instructions only.<br>2. Dedicated pre-retrieval scope control guardrail. | Dedicated pre-retrieval scope control component | Adds minor processing latency per query, but reliably prevents out-of-scope advice and unsafe responses. |

---

## Initial Requirements Traceability Matrix

| Objective | Requirement | Evaluation Criterion | Architecture Element | Later Evidence |
| :--- | :--- | :--- | :--- | :--- |
| **O1** | FR1, FR3 | Grounding & Source Citation | Scholarship PDF Knowledge Source + RAG Context Injector | Test set citation accuracy report & source match logs. |
| **O2** | RAI2, FR4 | Scope Boundaries & Refusals | Pre-retrieval Scope / Safety Control | Evaluation pass rate on 20 out-of-scope test prompts. |
| **O3** | NFR1, NFR2 | Response Latency & Answer Accuracy | Language Model Service + Evaluation Logging Point | Automated latency trace logs (p90) and evaluation rubric scores. |