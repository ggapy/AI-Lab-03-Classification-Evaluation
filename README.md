# AI Lab 03 — Classification Evaluation and Failure Simulation

## Overview

This hands-on n8n lab demonstrates how to evaluate a message-classification workflow while keeping **classification accuracy**, **evaluation coverage**, and **API failures** separate. It uses a controlled, synthetic test set and **does not call a live AI model** during the partial-failure simulation.

The goal is to show why high accuracy among completed predictions does not, by itself, demonstrate that every request was processed successfully.

## Scenario

A customer-message classifier routes messages to four categories:

- Billing
- Sales
- Support
- Other

The test set contains 15 manually designed messages with expected labels. The workflow simulates successful classification for the first 12 messages (using their expected labels), and simulated API failures for the remaining three.

## Workflow design

The n8n workflow branches after the test-case generator:

**Simulated prediction branch**

`Trigger → 10 Cases → Simulate Partial Results → Evaluate Predictions → Category Metrics → Confusion Matrix → Evaluation Report → Evaluation Coverage`

**Simulated failure branch**

`10 Cases → Simulate 3 API Failures → Capture API Failures → API Failure Summary`

**Unified reporting**

`Evaluation Coverage + API Failure Summary → Merge Evaluation Results → Unified Evaluation Report → Export Evaluation Report`

The two branches are combined into a single report. The export step writes a Markdown file for review and archival.

## Results (controlled simulation)

| Measurement | Result |
|---|---:|
| Expected test cases | 15 |
| Completed simulated predictions | 12 |
| Correct simulated predictions | 12 |
| Incorrect simulated predictions | 0 |
| Classification accuracy among completed predictions | 100% |
| Evaluation coverage | 80% |
| Missing predictions | 3 |
| Recorded simulated API failures | 3 |
| Missing predictions reconciled with simulated failures | 3 |
| Unexplained missing predictions | 0 |

### Classification results by category

| Category | Completed cases | Precision | Recall | F1 |
|---|---:|---:|---:|---:|
| Billing | 4 | 100% | 100% | 100% |
| Sales | 3 | 100% | 100% | 100% |
| Support | 3 | 100% | 100% | 100% |
| Other | 2 | 100% | 100% | 100% |

These perfect scores are **expected by design**: the simulated predictions reuse the expected labels. They do **not** measure real-model classification quality.

### Simulated API failures

| Test ID | Expected category | Simulated outcome |
|---|---|---|
| 13 | Billing | API failure |
| 14 | Other | API failure |
| 15 | Billing | API failure |

The three absent predictions correspond exactly to the three generated failure records. No unexplained missing predictions remained in this run.

## What this lab demonstrates

- **Evaluation logic:** compares predicted versus expected labels and produces per-category metrics and a confusion matrix.
- **Coverage tracking:** calculates completed predictions against the original set of 15 cases.
- **Failure capture:** preserves test IDs, expected categories, error messages, and timestamps in structured records.
- **Reconciliation:** checks whether missing predictions correspond to known simulated failures.
- **Reproducible reporting:** combines branches and exports a documented Markdown evaluation report.

## How to reproduce

1. Import `AI_Lab_03_Partial_Failure_Test_Public.json` into a **test** n8n environment.
2. Review the Code nodes and connections before execution. **The public JSON contains no OpenAI node or API credentials**; both the predictions and failures are simulated locally in Code nodes.
3. Run the manual trigger to generate 15 test cases and execute both simulated branches.
4. Inspect `Evaluate Predictions`, `Evaluation Coverage`, `API Failure Summary`, and `Unified Evaluation Report`.
5. Confirm the results above, then inspect the Markdown file from `Export Evaluation Report`.

The public workflow JSON was sanitized before sharing: an unused, disconnected OpenAI node and environment-specific identifiers were removed. Inspect any future exports separately before publishing, especially if the workflow is modified.

## Artifacts

- **n8n workflow JSON:** [AI_Lab_03_Partial_Failure_Test_Public.json](./AI_Lab_03_Partial_Failure_Test_Public.json) — sanitized, simulation-only public export.
- **Evaluation report:** [AI_Lab_03_Partial_Failure_Simulation_2026-11-11.md](./AI_Lab_03_Partial_Failure_Simulation_2026-11-11.md)
- **This README:** describes the setup, test design, and interpretation.

## Limitations and next steps

- The dataset is small and manually constructed; it is not representative of production traffic.
- Predictions were synthesized from known labels, so the accuracy and category metrics cannot validate model performance.
- API failures were deliberately simulated; this is **not** a live API reliability, latency, or throughput benchmark.
- A future test should use real model predictions, independently labeled examples, more varied edge cases, and operational measurements.
- Before adapting to production, ensure the reporting logic also handles a run with **zero API failures**, not just two nonempty branches.

---

**Status:** Completed controlled simulation. **Do not describe these percentages as live AI model performance or production reliability results.**
