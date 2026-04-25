# Experiment 0 — Sanity Check (Feasibility Check)

This notebook is part of the master's thesis:
**"Heterogeneous Graph Neural Networks for User Journey Modeling:
A Comparative Study with Sequential and Probabilistic Approaches"**
Transport and Telecommunication Institute (TSI), Riga, 2026.

**Purpose:** Confirm that the GA4 dataset contains a sufficient predictive
signal before proceeding to the main classification experiments.

## Task

Binary classification: purchase vs non-purchase at the full-session level
using static, aggregated session features.

## Data

Google Analytics 4 public e-commerce dataset:
`bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`

- 359,940 sessions · 92 days (Nov 2020 – Jan 2021)
- Conversion rate: 1.35% (4,848 purchase sessions)
- Requires Google Cloud Platform account for BigQuery access

## Models

| Model | Test ROC-AUC |
|---|---|
| Logistic Regression | 0.9823 |
| Random Forest | 0.9827 |

## Result

ROC-AUC > 0.98 for both models confirms the dataset is informative.
This result is not directly comparable to Experiments 1–3: binary
classification on complete sessions differs fundamentally from four-class
prefix-level classification. The sanity check is passed; the main
comparative line proceeds from Experiment 1.

## Notebook

`exp0_SanityCheck.ipynb` — all outputs are saved inline; no separate
data files required.
