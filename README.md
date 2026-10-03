# IntegrityInsight

Exam integrity analysis: simulation + ingestion + warehouse + quality + dashboards + collusion detection.

Source notebook: `IntegrityInsight_Connected_Fixed_Ready.ipynb` (28 cells: data simulators FR-1..FR-6, ingestion pipeline, star-schema transformation FR-7, data-quality suite FR-8, D6-D10 dashboards + collusion module).

## Requirements
- Python 3.10+
- Libraries in `requirements.txt` (numpy, pandas, scikit-learn, scipy, matplotlib, notebook)

## How to run
1. `pip install -r requirements.txt`
2. Copy `IntegrityInsight_Connected_Fixed_Ready.ipynb` into this folder root.
3. Open the notebook and run top to bottom.
4. For quick test set `FULL_RUN=False` (300 candidates, ~300k responses). Full run uses `FULL_RUN=True` with `SEED=42` (5000 candidates, 20 exams, 1000 items, 5M responses).
5. Outputs go to `integrityinsight_data/` (raw, staging, warehouse, validation) — this folder is git-ignored and not uploaded.

## Reproduce same results
- Fixed `SEED=42`.
- Stored notebook outputs show expected PASS states (FR-1, FR-3, FR-5, FR-6, FR-7 ingestion PASSED).
- Note: cells 15+ use `/content/...` paths and `google.colab` download — run in Google Colab for full compatibility, or adapt paths locally.

## Repo layout
- `src/` — source code split (simulators, ingestion, warehouse, analysis, reporting)
- `docs/` — metric dictionary + data contracts
- `data/` — local only, not uploaded (raw, staging, ground_truth)
- `dashboards/` — Power BI / Tableau / Streamlit outputs
