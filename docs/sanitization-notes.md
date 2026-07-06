# Sanitization Notes

## Purpose

This repository is intended to be a public, portfolio-safe version of the Project 3 implementation. The goal is to demonstrate architecture, workflow design, and evaluation discipline without publishing raw course materials, proprietary source files, credentials, personally identifiable information, or environment-specific runtime details.

## What Is Included

The public repository may include:

- sanitized n8n workflow JSON files
- selected slide screenshots exported from the final presentation
- high-level project documentation written for portfolio review
- summary-level metrics and architectural explanation

## What Is Not Included

The public repository should not include:

- raw SQLite databases
- raw CSV source files
- the source playbook PDF
- course-provided rubrics, templates, or solution guides
- unredacted screenshots
- customer names or personally identifiable information
- API keys, tokens, secrets, or credentials
- webhook IDs
- n8n instance IDs
- internal workflow IDs
- cached n8n workflow URLs
- local execution paths tied to the course lab environment

## Sanitized Workflow File Expectations

The final public workflow files should be named:

```text
workflows/WF1_customer_profile_lookup_sanitized.json
workflows/WF2_locker_availability_sanitized.json
workflows/WF3_main_runtime_pipeline_sanitized.json
workflows/WF4_evaluation_harness_sanitized.json
```

Before publishing, verify that each workflow:

- contains no credential blocks
- contains no credential IDs or credential names
- contains no webhook IDs
- contains no n8n instance IDs
- contains no top-level workflow IDs from the original environment
- contains no internal workflow URLs
- replaces lab file paths with placeholders
- is set inactive by default
- preserves the technical logic, prompts, node structure, routing, and evaluation logic

## Recommended Placeholder Values

Use generic placeholders such as:

```text
REPLACE_WITH_SHARED_DATA_PATH/customers.db
REPLACE_WITH_SHARED_DATA_PATH/delivery_logs.csv
REPLACE_WITH_SHARED_DATA_PATH/ground_truth.csv
REPLACE_WITH_SHARED_DATA_PATH/exception_resolution_playbook.pdf
REPLACE_WITH_IMPORTED_WF1_ID
REPLACE_WITH_IMPORTED_WF2_ID
REPLACE_WITH_IMPORTED_WF3_ID
```

## Why Full Prompts Are Preserved

The full sanitized prompts should remain in the workflow JSONs because they show the actual complexity of the agentic design: tool-use rules, structured output schemas, escalation policy, critic validation, safety instructions, and edge-case handling.

Sanitization should remove secrets and environment-specific values, not reduce the technical depth of the project.

## Final Public Review Checklist

Before switching the repository from private to public, open every file in GitHub and confirm:

- no secrets are present
- no personal data is present
- no raw course-provided data files are present
- screenshots do not expose credentials or PII
- workflow JSONs use placeholders for file paths and workflow references
- README links render correctly
- screenshot images display correctly
- docs are written in your own explanatory language
