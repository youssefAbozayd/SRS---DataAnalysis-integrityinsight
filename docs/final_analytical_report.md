# Final Analytical Report + Recommendations (D17)

> Filled from stored notebook outputs (300-candidate staged run). Cell 0 asserts validate the full 5000-candidate design; detailed deliverables below were generated on the staged subset: 300 candidates, 6000 sessions, 300000 responses.

## 1. What we analyzed
- Data: 9 raw tables (candidates, items, sessions, exam_responses, session_risk, proctoring_flags, review_verdicts, reviewers, infrastructure_cost).
- Pipeline: contract validation + ingestion (FR-6), star-schema warehouse with SCD Type-2 (FR-7), DQ suite FR-8 (123 tests), item analysis D11 (1000 items), cost model D12, metric dictionary D14 (24 metrics), access/retention D16, executive/reviewer/fairness dashboards D6-D8, collusion module D9 + case file D10.
- Scale in outputs: 326557 raw rows staged, 0 rejected; FACT_RESPONSE 300000, FACT_SESSION_RISK 6000, FACT_REVIEW 3795.

## 2. Findings (with evidence)
- F1 Ingestion clean: 9/9 tables SUCCESS, 0 rejected, staging integrity PASSED. Source: cells 12-14.
- F2 Warehouse valid: all FK checks PASS, DIM_EXAM/DIM_REVIEWER Type-2 PASS, DR-5 columns PASS. Source: cell 15.
- F3 DQ 100%: 123/123 passed, 6/6 corruptions detected (CORR-001..006). Source: cell 16.
- F4 Weakest flag: GAZE_OFF_SCREEN precision 0.3286 (95% CI 0.305-0.353, n=1467). Next PHONE_DETECTED 0.5473; strongest REMOTE_TOOL 0.8438, TAB_SWITCH 0.8003. Source: cell 23.
- F5 Review reliability substantial: double-review kappa 0.605, n_pairs 345; drift suspects reviewer_03, reviewer_05, reviewer_12; fatigue slope -0.00014/position (rho -0.033, p 0.0444). Source: cell 24.
- F6 Cost: total synthetic cost 879.0388; cost/session 0.1465, labour share 40%. What-if threshold 0.30 -> 2128 reviews vs 0.75 -> 22 reviews. Source: cells 19, 23-24.
- F7 Fairness alerts (threshold 1.25): lighting poor/good 1.295, recommendation HUMAN_REVIEW/NO_ACTION 1.77, exam_005/exam_004 1.267. Source: cell 25.
- F8 Collusion signals work: WAA AUC 0.901, timing 0.938, combined 0.958; 44 suspicious edges, components [66,22]; P(high risk|high WAA) 0.83; 175 collusion-only catches (WAA high, risk<0.5). Case cand_00051-cand_00086 WAA 0.917. Bonferroni hits 0, BH hits 0 (conservative). Source: cells 26-27.

## 3. Analysis (what results mean)
- GAZE_OFF_SCREEN drives most overturns; keeping it at full weight wastes review capacity.
- Kappa 0.605 means reviewers agree substantially but not perfectly — keep double-review for calibration, do not auto-punish on single verdict.
- Drift + fatigue signals are small but real — rotate reviewers and cap consecutive reviews.
- Cost/what-if shows threshold is the main capacity lever, not per-review speed.
- Fairness gaps (lighting, exam) mean flags confound environment with misconduct — adjust before any high-stakes decision.
- Stats catch 175 cases cameras miss (triangulation) — combined WAA+timing (+proctor risk) is the right detector, Bonferroni for accusations, BH for investigation queue.

## 4. Recommendations
- R1 Down-weight/suppress GAZE_OFF_SCREEN; route PHONE_DETECTED to senior review. Based on F4.
- R2 Keep PRIORITY_REVIEW threshold high (22/6000 sessions); use threshold 0.50 as default operating point (446 reviews, precision 0.462). Based on F5-F6.
- R3 Calibrate reviewers: retrain reviewer_03/05/12, enforce breaks after ~30 consecutive reviews, keep 10% double-review. Based on F5.
- R4 Fairness fix: normalize for lighting/webcam/noise before scoring; audit exam_005 vs exam_004. Based on F7.
- R5 Adopt combined collusion score (AUC 0.958) with Bonferroni accusation list + BH investigation queue; open case cand_00051-cand_00086 as worked example. Based on F8.
- R6 Keep DQ 123-test gate + corruption demos as release gate; next full 5000-candidate run must reproduce run_summary.json before D18 demo.
