# Experiment 1 — Sequence-Only Baselines

A double-degree master's thesis submitted to the Transport and
Telecommunication Institute (TSI), Riga, and the University of the
West of England (UWE Bristol), 2026.

**Thesis title:**
"Heterogeneous Graph Neural Networks for User Journey Modeling:
A Comparative Study with Sequential and Probabilistic Approaches"

**Purpose:** Establish a performance ceiling for prefix-level session
classification using strictly minimal input — event name sequences only.

## Task

Four-class prefix-level classification: Browser / Researcher / Intent / Buyer.
For each session of length L, prefixes t = 1…min(L, T_max) are generated.
The model observes only the ordered sequence of event names up to prefix
length t and predicts the full-session class label.

## Data

Google Analytics 4 public e-commerce dataset:
`bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`

- 360,129 sessions · 92 days (Nov 2020 – Jan 2021)
- Temporal split 70/15/15 by session end time
- T_max = 43 (p95 of train session lengths)
- 3,325,933 prefix rows total

## Class Distribution

| Class | Sessions | % |
|---|---|---|
| Browser | 319,848 | 88.81% |
| Researcher | 19,943 | 5.54% |
| Intent | 15,490 | 4.30% |
| Buyer | 4,848 | 1.35% |

## Models and Results

| Model | Test Macro-F1 |
|---|---|
| Majority baseline | 0.1990 |
| Heuristic baseline | 0.3761 |
| Markov(1) | 0.3186 |
| SASRec Base | 0.4176 ± 0.0011 |

Primary metric: Macro-F1 (unweighted mean across 4 classes).
SASRec results are mean ± std across 3 seeds (42, 123, 456).

## Notebook

`exp1_SequentialBaselines.ipynb` — all outputs are saved inline; no
separate data files required. BigQuery access required to rerun data
extraction (Section 1).
