# Institutional Data Analysis Report — Template (D13)

> Automated template. Do NOT write numbers by hand. Each `{{placeholder}}` is filled automatically from the data / dashboard source listed under it.

## 1. Executive Summary
- Reporting period: `{{reporting_period}}` | Source: `warehouse/dim_date.csv`
- Total candidates: `{{total_candidates}}` | Source: `warehouse/dimensions/dim_candidate.csv`
- Total sessions: `{{total_sessions}}` | Source: `warehouse/facts/fact_session_risk.csv`
- Total responses: `{{total_responses}}` | Source: `warehouse/facts/fact_response.csv`
- Overall flag rate: `{{flag_rate}}` | Source: `staging/proctoring_flags.csv`
- High-risk session share: `{{high_risk_share}}` | Source: `warehouse/facts/fact_session_risk.csv`

## 2. Data Quality
- Tables validated: `{{tables_validated}} / {{tables_total}}` | Source: `validation/ingestion_audit_log.csv`
- Total rejected rows: `{{total_rejected_rows}}` | Source: `validation/ingestion_audit_log.csv`
- Staging integrity check: `{{staging_integrity_status}}` | Source: `validation` (integrity check cell)
- Flag precision report available: `{{flag_precision_report_path}}` | Source: `validation/flag_precision_report.csv`
- Reviewer agreement report available: `{{reviewer_agreement_report_path}}` | Source: `validation/reviewer_agreement_report.csv`

## 3. Key Metrics
| Metric | Value (auto) | Source |
|---|---|---|
| Avg accuracy | `{{avg_accuracy}}` | `fact_response.csv` |
| Avg response time (ms) | `{{avg_response_time_ms}}` | `fact_response.csv` |
| Double-review case rate | `{{double_review_rate}}` | `fact_review.csv` |
| Double-review Cohen's kappa | `{{double_review_kappa}}` | `validation/run_summary.json` |
| Risk-only AUC (baseline) | `{{risk_auc}}` | `validation/run_summary.json` |
| Total review labor cost | `{{total_review_labor_cost}}` | `staging/infrastructure_cost.csv` |

## 4. Findings
- Finding 1: `{{finding_1}}` | Evidence: `{{finding_1_metric}}` from `{{finding_1_source}}`
- Finding 2: `{{finding_2}}` | Evidence: `{{finding_2_metric}}` from `{{finding_2_source}}`
- Finding 3: `{{finding_3}}` | Evidence: `{{finding_3_metric}}` from `{{finding_3_source}}`

## 5. Analysis
- Interpretation 1: `{{analysis_1}}` (linked to `{{finding_1}}`)
- Interpretation 2: `{{analysis_2}}` (linked to `{{finding_2}}`)
- Limitations: `{{limitations}}` | Source: DQ suite `validation/data_quality/dq_test_results.csv`

## 6. Recommendations
- Recommendation 1: `{{recommendation_1}}` (based on `{{finding_1}}`)
- Recommendation 2: `{{recommendation_2}}` (based on `{{finding_2}}`)
- Owner / next review date: `{{owner}}` / `{{next_review_date}}`

---
*Generated from placeholders only. See D17 for the filled final report.*
