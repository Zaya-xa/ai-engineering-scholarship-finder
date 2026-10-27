# ai-engineering-scholarship-finder
# AI Scholarship Finder
> Answers student queries about scholarship eligibility, award criteria, and application deadlines, grounded in official financial aid PDF documents.

## Problem Statement
Students struggle to locate and verify scholarship information because requirements are scattered across multiple complex PDFs and websites. AI Scholarship Finder provides instant, document-grounded answers to match students with the right funding opportunities.

## Evidence of the Problem
- Scholarship guidelines and qualification rules are distributed across multiple separate documents.
- Students frequently miss application deadlines or apply for incorrect eligibility tiers due to information fragmentation.

## Initial Related Work / Existing Approaches
- Manual university portals — authoritative, but fragmented and difficult to search.
- Rule-based scholarship matchers — structured, but rigid and often outdated.
- General-purpose AI assistants — flexible, but prone to hallucinating deadlines or non-existent funding programs.

## Engineering Gap / Limitation
Existing tools are either static and hard to navigate, or flexile LLMs that lack strict grounding in official, up-to-date local financial aid documents.

## Project Objectives
- O1: Design a document-grounded AI scholarship advising solution.
- O2: Develop the solution with retrieval mechanisms and guardrails to prevent deadline hallucination.
- O3: Evaluate answer accuracy, groundedness, latency, and safety.

## Target Users
Undergraduate students seeking scholarships, bursaries, or financial aid.

## Data Sources
- JPA Scholarship Guidelines PDF (Official Portal URL)
- University Endowment Handbook PDF (University Portal URL)

## Weekly Progress
| Week | Focus | Deliverable | Status |
|------|-------|-------------|--------|
| W1 | System map + project scope | README + docs | ✅ |