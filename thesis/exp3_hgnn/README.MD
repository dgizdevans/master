# Experiment 3 — Heterogeneous Graph Neural Network (HeteroGraphSAGE)

A double-degree master's thesis submitted to the Transport and
Telecommunication Institute (TSI), Riga, and the University of the
West of England (UWE Bristol), 2026.

**Thesis title:**
"Heterogeneous Graph Neural Networks for User Journey Modeling:
A Comparative Study with Sequential and Probabilistic Approaches"

**Purpose:** Evaluate whether a heterogeneous graph neural network that
explicitly models structural relationships between events, pages, and items
improves prefix-level session classification over the best non-structural
baseline (SASRec +Time, Macro-F1 = 0.5731).

## Task

Four-class prefix-level classification: Browser / Researcher / Intent / Buyer.
Same protocol as Experiments 1–2: prefixes t = 1…min(L, T_max), temporal
split 70/15/15, primary metric Macro-F1.

## Data

Google Analytics 4 public e-commerce dataset:
`bigquery-public-data.ga4_obfuscated_sample_ecommerce.events_*`

- 327,283 sessions · 92 days (Nov 2020 – Jan 2021)
- Temporal split 70/15/15 by session end time
- T_max = 43 (p95 of train session lengths)
- 1,277,287 prefix subgraphs total

## Graph Schema

Each session prefix is converted into a heterogeneous graph:

| Node types | Event · Page · Item |
|---|---|
| Edge types | next\_event · on\_page · view\_item\_of · add\_to\_cart\_of · remove\_from\_cart\_of · begin\_checkout\_of · purchase\_item\_of |

Readout: last event node embedding + session-level feature vector → MLP classifier.

## Model

HeteroConv + SAGEConv, 2 layers, hidden dim = 64, dropout = 0.3.
Trained on NVIDIA L4 (CUDA). Three seeds (42, 123, 456).

## Results

| Variant | Test Macro-F1 |
|---|---|
| Full model | **0.6383 ± 0.0059** |
| no\_delta\_t | 0.6361 ± 0.0031 |
| no\_page\_item | 0.6325 ± 0.0073 |
| no\_session\_features | 0.6081 ± 0.0031 |

## Per-Class F1 (Full Model)

| Class | F1 |
|---|---|
| Browser | 0.890 ± 0.004 |
| Researcher | 0.652 ± 0.006 |
| Intent | 0.573 ± 0.014 |
| Buyer | 0.438 ± 0.005 |

## Key Finding

HeteroGraphSAGE outperforms the best non-structural baseline (SASRec +Time)
by +0.065 Macro-F1. Minority class gains: Buyer +0.104, Intent +0.093.
The ablation shows session-level features contribute the most (−0.030 without
them), while shared Page/Item structure provides an independent but smaller
gain (−0.006).

## Notebook

`exp3_HeteroGraphSAGE.ipynb` — all outputs are saved inline; no separate
data files required. GPU (NVIDIA L4) required to rerun training.
BigQuery access required to rerun data extraction.
