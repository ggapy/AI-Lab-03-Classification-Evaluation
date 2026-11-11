> **SIMULATION ONLY — No real OpenAI API calls were made in this evaluation.**

# AI Classification Evaluation Report

Evaluation date (UTC): 2026-11-11T19:36:20.758Z
Model: Not invoked (simulated predictions)
Workflow: AI Lab 03 - Classification Evaluation

## Overall Results

Total test cases: 12
Correct predictions: 12
Incorrect predictions: 0
Accuracy: 100%

## Category Performance

| Category | Cases | Precision | Recall | F1 |
|---|---:|---:|---:|---:|
| Billing | 4 | 100% | 100% | 100% |
| Sales | 3 | 100% | 100% | 100% |
| Support | 3 | 100% | 100% | 100% |
| Other | 2 | 100% | 100% | 100% |

## Confusion Matrix

Rows = actual category; columns = predicted category.

| Actual | Billing | Sales | Support | Other |
|---|---:|---:|---:|---:|
| Billing | 4 | 0 | 0 | 0 |
| Sales | 0 | 3 | 0 | 0 |
| Support | 0 | 0 | 3 | 0 |
| Other | 0 | 0 | 0 | 2 |

## Failed Test Cases

No classification errors detected.

## Evaluation Limitations

- Small, manually designed test dataset.
- Results do not guarantee production accuracy.
- Real-world customer messages require further testing.
- API reliability and latency are not evaluated.
- Future prompt or model changes require regression tests.

## Evaluation Coverage

Expected test cases: 15
Completed predictions: 12
Missing predictions: 3
Evaluation coverage: 80%
Coverage status: partial

Missing test IDs: 13, 14, 15

Missing predictions require investigation.
They are not automatically classified as API failures.

## Simulated API Failure Analysis

Simulated API failures: 3
Missing predictions: 3
Failures matching missing predictions: 3
Unexplained missing predictions: 0

### Failures by Category

| Category | Failures |
|---|---:|
| Billing | 2 |
| Sales | 0 |
| Support | 0 |
| Other | 1 |

Unknown categories: 0

### Affected Test Cases

- Test 13: Billing — Simulated OpenAI API failure
- Test 14: Other — Simulated OpenAI API failure
- Test 15: Billing — Simulated OpenAI API failure

### Unexplained Missing Predictions

None

### Evaluation Interpretation

Classification accuracy: 100%
Evaluation coverage: 80%

This is a controlled simulation, not a production reliability measurement.
Predictions were generated from expected labels.
API failures were simulated rather than produced by OpenAI.