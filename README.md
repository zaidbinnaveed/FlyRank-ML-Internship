# FlyRank ML Internship — Content Opportunity Scoring

A reproducible machine-learning capstone that ranks existing content for editorial refresh review using anonymized search and engagement signals.

The system is decision support: it identifies review candidates and explains the signals behind each recommendation. It does **not** predict Google's algorithm, prove that a refresh will cause traffic growth, or automate publishing.

## Verified result

The committed model report is generated from the bundled 30,000-row anonymized dataset using a client-group holdout.

| Model | ROC AUC | Average precision | Precision@50 | Recall | F1 |
|---|---:|---:|---:|---:|---:|
| Random forest | 0.750 | 0.618 | **0.740** | 0.744 | 0.640 |
| Decision tree | 0.742 | 0.575 | 0.540 | 0.716 | 0.634 |
| Logistic regression | 0.700 | 0.522 | 0.400 | 0.567 | 0.566 |
| Transparent rule baseline | 0.627 | 0.468 | 0.240 | — | — |

The random forest is selected by `precision_at_50`, matching the operational goal of giving reviewers a useful top-of-queue shortlist. See [the full generated model report](outputs/model_report.md).

## Pipeline

```text
anonymized input
  → schema and leakage checks
  → transparent feature preparation
  → rule baseline
  → grouped model validation
  → ranked opportunity score
  → reason codes and editorial action
  → CSV queue, charts, and report
```

## Run the reproducible pipeline

```bash
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
python scripts/run_all.py
```

The pipeline reads `data/raw/content_refresh_anonymized.csv` and regenerates the artifacts under `outputs/`.

## Repository map

```text
data/raw/                    anonymized starter data
notebooks/                   guided analysis notebooks
scripts/                     reproducible feature, model, and report pipeline
outputs/                     generated model report, queue sample, and charts
docs/                        research paper and supporting guides
work/                        weekly internship submissions and capstone notebook
skills/                      focused workflow instructions used during the track
submission/paper_url.txt     deployed paper URL
```

## Data-safety rules

The public dataset removes client names, domains, URLs, titles, keywords, and raw queries. Hashed identifiers remain pseudonymous and are used only for grouping, joining, and validation—not as model features.

Read [DATA_USE.md](DATA_USE.md) before replacing or extending the data. Never commit private client data or paste it into unapproved third-party services.

## Interpretation

The safest use of the output is human review:

1. inspect high-confidence rows;
2. verify the page and editorial context;
3. treat reason codes as review prompts;
4. measure post-refresh outcomes separately.

The model observes association in historical signals. It does not establish causal refresh impact.
