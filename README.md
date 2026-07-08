# Applied AI Delivery Exception Automation

Portfolio-safe repository for **Project 3: AI-Powered Last-Mile Delivery Exception Handling Automation** from the UT Austin Post Graduate Program in AI Agents for Business Applications.

This project demonstrates a controlled proof of concept multi-agent workflow that automates last-mile delivery exception handling using n8n, tool-calling agents, retrieval-augmented generation, deterministic escalation rules, critic validation, and an evaluation harness.

> **Portfolio note:** This repository is intended to show implementation approach, architecture, workflow orchestration, evaluation discipline, and AI program delivery thinking. It does not include proprietary course source files, raw datasets, customer records, credentials, API keys, or private execution data.

---

## Recruiter Quick Scan

This repository is designed for recruiters, hiring managers, and delivery leaders who want to see how I think about applied AI delivery, not just whether a workflow runs.

Best-fit role signals:

- AI Program Manager
- Applied AI Transformation Program Manager
- Technical Program Manager
- IT Program Manager for AI-enabled workflow delivery
- PMO or Delivery Manager supporting automation, governance, and pilot readiness

What this project shows:

- Business problem framing tied to operational KPIs
- Modular n8n workflow orchestration
- Tool-calling agent design
- Retrieval-augmented policy grounding
- Deterministic escalation rules before LLM reasoning
- Critic validation before customer communication
- Evaluation harness design and benchmark results
- Sanitized, portfolio-safe public documentation

What this project does not claim:

- It is not positioned as a production-ready system.
- It is not intended to show deep machine learning engineering.
- It does not include proprietary course files, raw data, credentials, customer records, or private execution payloads.

---

## Project Overview

Last-mile delivery exceptions create operational bottlenecks, inconsistent resolution decisions, delayed customer communications, unnecessary reattempt costs, and customer churn risk. Examples include failed delivery attempts, address issues, damaged packages, refused deliveries, weather delays, and locker reroute decisions.

The objective of this proof of concept was to build an AI-powered exception-handling pipeline that can:

- ingest noisy delivery status logs,
- consolidate duplicate or multi-row shipment events,
- identify actionable exceptions versus routine operational noise,
- retrieve policy guidance from an exception-resolution playbook,
- use customer and locker data through controlled tool workflows,
- apply deterministic escalation rules,
- select the appropriate resolution action,
- generate customer-facing communication,
- validate outputs through critic agents, and
- evaluate results across shipment-level test cases.

---

## Business Problem

Delivery operations teams often rely on manual triage to interpret shipment logs, driver notes, customer history, package constraints, locker availability, and internal policy rules. This slows resolution, creates inconsistent decisions, and increases support volume.

Key business KPIs addressed by this project include:

- exception resolution time,
- escalation accuracy,
- customer communication quality,
- cost per exception,
- customer retention risk,
- auditability of AI-assisted decisions.

The proof of concept frames the AI system as a controlled decision-support workflow rather than a claim of unrestricted production readiness.

---

## Program Delivery Relevance

This project connects applied AI implementation with the delivery controls expected in enterprise environments. The value is not only the agentic workflow, but the way the workflow is structured for governance, escalation, validation, review, and pilot readiness.

Program and PMO practices reflected in the project:

- clear business problem definition,
- measurable success criteria,
- controlled tool access,
- deterministic business rules,
- maker and checker validation,
- documented limitations,
- privacy-aware sanitization,
- benchmark evaluation,
- human-in-the-loop pilot path.

This is the connection point to my broader background in IT program delivery, PMO governance, customer-facing implementation, risk management, executive visibility, and service restoration.

---

## Solution Architecture

The solution is organized into four cooperating n8n workflows.

| Workflow | Purpose | Portfolio Value |
|---|---|---|
| WF1 Customer Profile Lookup | Callable tool workflow for customer tier, preferences, exception history, active credit, and PII-controlled profile data | Demonstrates controlled data access and PII-aware tool design |
| WF2 Locker Availability | Callable tool workflow for locker capacity, package-size eligibility, and reroute feasibility | Demonstrates deterministic operational tool logic |
| WF3 Main Runtime Pipeline | End-to-end exception pipeline with RAG, preprocessing, guardrails, escalation logic, resolution agent, critic agent, communication agent, and final output | Demonstrates complex agentic workflow orchestration |
| WF4 Evaluation Harness | Batch evaluation workflow that runs WF3 across test cases, judges coherence, combines predictions, and computes metrics | Demonstrates evaluation discipline and observability |

---

## Multi-Agent Design

The main runtime pipeline uses a maker/checker pattern.

### Resolution Agent

Classifies whether a shipment event is an actionable exception and selects the correct resolution, such as:

- `RESCHEDULE`,
- `REPLACE`,
- `REROUTE_TO_LOCKER`,
- `RETURN_TO_SENDER`,
- `N/A` for routine events.

The Resolution Agent uses customer profile data, locker availability, deterministic escalation signals, package constraints, and playbook-guided policy reasoning.

### Critic-Resolution Agent

Validates the Resolution Agent output against policy, tool usage, escalation rules, customer facts, and approved citation labels. It returns an accept, revise, or escalate decision before the workflow proceeds.

### Communication Agent

Generates customer-facing communication when the final approved resolution is an exception. It applies tone and channel logic based on customer tier and communication preference.

### Critic-Communication Agent

Validates the customer message for completeness, tone, safety, required next steps, and consistency with the approved resolution.

---

## Retrieval-Augmented Generation

The workflow ingests an exception-resolution playbook and builds an in-memory vector store for policy retrieval. The critic-resolution agent uses the playbook search tool to validate whether resolution decisions are supported by the relevant policy guidance.

RAG components include:

- PDF playbook ingestion,
- recursive text splitting,
- OpenAI embeddings,
- in-memory vector store,
- playbook search tool used by the critic agent.

---

## Deterministic Escalation Logic

Escalation rules are handled through deterministic code before LLM reasoning. This keeps policy-sensitive decisions grounded in explicit business rules.

Example escalation triggers include:

- third failed delivery attempt,
- VIP customer with three or more exceptions in the prior 90 days,
- damaged perishable package,
- perishable weather delay greater than four hours,
- vacant or demolished address risk,
- standard customer with more than five exceptions in the prior 90 days,
- premium customer with perishable weather delay requiring discretionary review.

Automatic escalation takes precedence over discretionary escalation when both apply.

---

## Evaluation Results

The evaluation harness ran the main runtime pipeline across a curated shipment-level benchmark.

| Metric | Result |
|---|---:|
| Number of shipments | 10 |
| Task completion | 100% |
| Escalation accuracy | 100% |
| Resolution accuracy | 100% |
| Tone accuracy | 100% |
| Tool call accuracy | 100% |
| Mean reasoning coherence | 5.0 / 5 |

These results indicate that the proof of concept matched all expected outcomes in the curated benchmark. The appropriate next step would be a controlled shadow pilot with broader edge-case testing, live operational constraints, monitoring, and human-in-the-loop review.

---

## Governance and Pilot Readiness

A production path would require more than successful benchmark execution. Before any operational use, this workflow would need broader test coverage, live data validation, privacy and access reviews, monitoring, audit logging, support procedures, and human dispatcher review.

Recommended pilot controls:

- expand test cases beyond the curated benchmark,
- evaluate edge cases and failure modes,
- validate tool behavior under latency and outage conditions,
- confirm access controls and PII handling,
- log decision inputs, tool calls, validation outputs, and final recommendations,
- compare AI recommendations against human dispatcher decisions,
- use human review before any automated customer-facing action.

---

## Repository Structure

```text
README.md
/workflows
  WF1_customer_profile_lookup_sanitized.json
  WF2_locker_availability_sanitized.json
  WF3_main_runtime_pipeline_sanitized.json
  WF4_evaluation_harness_sanitized.json

/screenshots
  slide_03_executive_summary.png
  slide_04_business_problem.png
  slide_13_multi_agent_architecture.png
  slide_36_main_runtime_pipeline.png
  slide_29_final_metrics.png

/docs
  project-summary.md
  architecture-overview.md
  evaluation-results.md
  sanitization-notes.md
```

---

## Recommended Reviewer Path

For a quick review, start with these files in this order:

1. `README.md` for the business problem, architecture, evaluation summary, and portfolio positioning.
2. `screenshots/slide_03_executive_summary.png` for the executive summary and benchmark scope.
3. `screenshots/slide_13_multi_agent_architecture.png` for the maker/checker architecture.
4. `screenshots/slide_36_main_runtime_pipeline.png` for workflow complexity.
5. `docs/evaluation-results.md` for evaluation detail and limitations.
6. `docs/sanitization-notes.md` for public release controls.

---

## Screenshots

The screenshots folder is intended to highlight the portfolio story without requiring reviewers to open every workflow file.

Recommended screenshots:

1. **Executive Summary** shows benchmark results and scope.
2. **Business Problem** shows KPI alignment and operational value.
3. **Multi-Agent Architecture** shows maker/checker agent design.
4. **Main Runtime Pipeline** shows the full n8n workflow complexity.
5. **Final Metrics** shows evaluation results and measured outcomes.

---

## What Is Included

This repository may include:

- sanitized n8n workflow JSON files,
- selected slide screenshots,
- architecture overview documentation,
- evaluation summary documentation,
- sanitization notes,
- portfolio-safe project explanation.

---

## What Is Not Included

This repository intentionally excludes:

- raw course-provided datasets,
- SQLite database files,
- delivery log CSV files,
- ground-truth CSV files,
- proprietary playbook PDFs,
- proprietary course templates or rubrics,
- API keys,
- credential IDs,
- webhook URLs,
- internal n8n instance IDs,
- private execution payloads,
- customer PII.

---

## Sanitization Summary

The workflow JSONs should be sanitized before public release. Sanitization should remove or replace:

- n8n workflow IDs,
- node UUIDs where appropriate,
- credential blocks,
- OpenAI credential names and IDs,
- webhook IDs,
- cached workflow URLs,
- internal workflow references,
- local file paths,
- instance metadata,
- active execution settings.

The full prompts, routing logic, escalation rules, and evaluation logic should remain intact unless they contain private, proprietary, or sensitive content. The purpose of sanitization is to remove secrets and environment-specific details, not to reduce the technical complexity of the implementation.

---

## Skills Demonstrated

- Agentic AI workflow design
- n8n workflow orchestration
- Retrieval-augmented generation
- Tool-calling agents
- Critic agent validation
- Deterministic escalation logic
- PII-aware data access
- Structured outputs
- Evaluation harness design
- Test case execution
- Observability and traceability
- AI program delivery and governance thinking
- Pilot-readiness planning
- Human-in-the-loop review design

---

## Limitations and Next Steps

This project is a controlled proof of concept based on a curated benchmark. It is not positioned as production ready without additional validation.

Recommended next steps include:

- expand the test dataset beyond 10 curated shipments,
- add more exception categories and edge cases,
- test with live or near-real-time delivery feeds,
- monitor latency and tool failures,
- add stronger audit logging,
- apply formal PII and access-control reviews,
- run a shadow pilot with human dispatcher review,
- compare AI recommendations against human decisions before automation.

---

## Portfolio Positioning

This project demonstrates practical AI program delivery by connecting business problem framing, workflow architecture, agentic AI design, operational rules, security considerations, evaluation discipline, and pilot-readiness thinking.

It is intended to show that the builder can move beyond conceptual AI use cases and design a structured, testable, and auditable workflow suitable for controlled pilot evaluation.
