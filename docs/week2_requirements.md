# Section 0 — Project Framing & Application Scope Checkpoint

| Field | Description |
| :--- | :--- |
| **Problem Evidence** | Official scholarship guidelines, eligibility criteria, and application rules are distributed across separate institutional PDFs and portals. Students frequently misinterpret qualification tiers or miss critical application deadlines due to fragmented information sources. |
| **Existing Approaches** | 1. Manual search via university financial aid portals — authoritative, but fragmented and time-consuming to navigate.<br>2. Static scholarship aggregator platforms — structured, but rigid and often outdated.<br>3. General-purpose AI assistants (e.g., ChatGPT) — flexible, but risk hallucinating deadlines or eligibility rules not grounded in local official PDFs. |
| **Project / Engineering Gap** | Existing tools are either static and hard to navigate, or flexible LLMs that lack strict grounding and verifiable citations from official, up-to-date local financial aid documents. |
| **Objective O1** | To design a document-grounded AI scholarship assistant based on official financial aid PDFs. |
| **Objective O2** | To develop the proposed solution using retrieval-augmented generation (RAG) with guardrails against fabricated deadlines and out-of-scope requests. |
| **Objective O3** | To evaluate the proposed solution in terms of answer accuracy, groundedness, retrieval latency, and safety. |
| **Intended Users** | Undergraduate students seeking financial aid, university endowments, or government scholarships. |
| **Supported Tasks** | Answering eligibility criteria questions, checking application deadlines, listing required application documents, and comparing award terms across available scholarships. |
| **Information Domain** | Publicly accessible Malaysian scholarship PDFs, university endowment handbooks, and government financial aid guidelines. |
| **Operating Context** | Web-based Q&A application accessible to students via desktop or mobile browsers. |
| **Important Constraints** | Must use publicly accessible PDFs only; zero budget for proprietary database infrastructure; strict reliance on document context to prevent hallucination. |
| **Explicit Out-of-Scope Tasks** | 1. The system shall NOT process or submit scholarship applications on behalf of students.<br>2. The system shall NOT guarantee scholarship approval or award outcomes.<br>3. The system shall NOT provide personal financial advice, loan management, or legal counseling. |
| **Evaluation Focus** | Determining whether RAG grounded in official PDFs eliminates deadline/eligibility hallucinations while delivering sub-3-second responses. |

---

# Requirements Specification — AI Scholarship Finder
Version: 1.0

## Section 1 — Functional Requirements (FR)

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
| :--- | :--- | :--- |
| **FR1** | Answer student queries regarding scholarship eligibility criteria, income caps, and CGPA requirements using retrieved official PDF context. | Invent eligibility criteria or academic thresholds not present in the source documents. |
| **FR2** | Extract and display official application submission deadlines and key milestone dates from scholarship documents. | State or estimate a deadline if it is not explicitly documented in the retrieved text. |
| **FR3** | Provide a source reference (document title, section/page number) for every answer derived from official scholarship documents. | Present unsupported information as if it came from an approved source document. |
| **FR4** | Decline queries that fall outside scholarship and financial aid advising and redirect users to official university administrative channels. | Provide legal advice, academic course advising, personal loans counseling, or guaranteed application outcomes. |
| **FR5** | Present scholarship requirements as clear, structured bulleted lists or checklists formatted for undergraduate students. | - |

---

## Section 2 — Non-Functional Requirements (NFR)

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **NFR1** | Performance | Interactive query responses shall remain within the agreed latency target. | Measure end-to-end response time over a 30-query test set. | p90 latency | < 3,000 ms |
| **NFR2** | Correctness | Answers shall be factually accurate and consistent with official PDF guidelines. | Score a test evaluation set using a verified key rubric. | Correct response rate (%) | ≥ 85% |
| **NFR3** | Cost | Inference and embedding costs shall stay within student project limits. | Track API token usage across evaluation runs. | Cost per 100 queries | < US$0.30 per 100 queries |
| **NFR4** | Maintainability | New scholarship PDFs shall be ingested into the system without rebuilding core code. | Measure time required to parse and embed a new PDF document. | Document ingestion time | < 5 minutes |

---

## Section 3 — Responsible AI Requirements (RAI)

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RAI1** | Fairness | System accuracy shall not vary significantly across different study faculties or background tiers. | Compare query accuracy rates across STEM vs Non-STEM scholarship query sets. | Accuracy gap between academic fields | ≤ 8 percentage points |
| **RAI2** | Safety / Scope | The system shall refuse out-of-scope queries (e.g., legal, mental health, general chat) and redirect appropriately. | Test the system with a set of 20 out-of-scope and adversarial prompts. | Refusal-and-redirect success rate | ≥ 95% |
| **RAI3** | Privacy | The system shall not store or transmit student PII (MyKad numbers, bank accounts) to external model APIs. | Inspect outgoing payload logs during test sessions containing dummy PII. | Number of PII data leaks detected | 0 |
| **RAI4** | Transparency / Grounding | Answers must contain verifiable citations and indicate when information is missing from documents. | Inspect 50 generated responses for source presence and document alignment. | Citation presence rate; Source match rate | 100% citation presence; ≥95% source match |