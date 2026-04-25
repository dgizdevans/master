# Experiment 2 — Enriched Baselines

This notebook is part of the master's thesis:
**"Heterogeneous Graph Neural Networks for User Journey Modeling:
A Comparative Study with Sequential and Probabilistic Approaches"**
Transport and Telecommunication Institute (TSI), Riga, 2026.

**Purpose:** Evaluate whether enriching session prefix representations
with temporal intervals, contextual features, and higher-order sequence
models improves prefix-level classification over the Experiment 1 baseline.

## Task

Four-class prefix-level classification: Browser / Researcher / Intent / Buyer.
Same protocol as Experiment 1: prefixes t = 1…min(L, T_max), temporal
split 70/15/15, primary metric Macro-F1.

## Data

Google Analytics 4 public e-commerce dataset:
`bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`

- 360,129 sessions · 92 days (Nov 2020 – Jan 2021)
- Temporal split 70/15/15 by session end time
- T_max = 43 (p95 of train session lengths)
- 497,852 test prefix rows

## Models and Results

| Model | Test Macro-F1 |
|---|---|
| Markov(1) | 0.3186 |
| Markov(2) | 0.3794 |
| Markov(3) | 0.4221 |
| LightGBM | 0.5632 |
| SASRec Base | 0.5668 ± 0.0047 |
| SASRec +Time | **0.5731 ± 0.0021** |
| SASRec +Context | 0.5694 ± 0.0019 |
| SASRec +Time+Context | 0.5688 ± 0.0059 |

Primary metric: Macro-F1. SASRec results are mean ± std across 3 seeds.
Best result: **SASRec +Time (0.5731 ± 0.0021)**.

## Key Finding

LightGBM (0.5632) and SASRec +Time (0.5731) converge within 0.01 Macro-F1
despite fundamentally different architectures. Pairwise prediction agreement
between LightGBM and SASRec Base reaches 0.918, suggesting a representational
bottleneck in flat sequence encoding rather than model-specific limitations.

## Notebook

`exp2_EnrichedBaselines.ipynb` — all outputs are saved inline; no separate
data files required. GPU (NVIDIA L4) used for SASRec training. BigQuery
access required to rerun data extraction.
