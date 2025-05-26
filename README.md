---
title: 🏀 InjuryDetection
emoji: 🏀
colorFrom: red
colorTo: red
sdk: docker
app_port: 8501
tags:
  - streamlit
  - transformers
  - nlp
  - pytorch
  - nba
  - healthcare
  - sports
pinned: false
description: Predict NBA injury type and duration using a fine-tuned DistilBERT + structured features.

---

# 🏀 Injury Detection & Recovery Duration Estimator

A powerful **Streamlit app** powered by a fine-tuned **DistilBERT** transformer that predicts:

- 🔍 **Injury Type** (e.g., bone, muscle, joint, illness, concussion)
- ⏳ **Recovery Duration**:  
  - `short` (< 7 days)  
  - `medium` (7–45 days)  
  - `long` (> 45 days)
  
---

## 🚀 Why This Project?

NBA injuries are unpredictable, and doctors often rely on vague reports or historical intuition. I wanted to go beyond zero-shot text classification by:

- Cleaning and normalizing raw injury logs (1950–2022)
- Labeling 8K+ examples by type and duration
- Incrementally testing feature combinations
- Analyzing attention weights and feature influence
- Making predictions explainable and interactive via Streamlit

---

## 🧠 Model Highlights

| Component         | Description                             |
|------------------|-----------------------------------------|
| Model            | `distilbert-base-uncased`               |
| Task             | Dual classification                     |
| Inputs           | Text + prior injuries, position, type ID|
| Output Heads     | `label_type_id` and `label_duration_id` |
| Loss             | Weighted cross-entropy (multi-task)     |
| Extras           | Attention score input for interpretability|

---

## 💡 Features

- 📝 **Free-text input** for injury reports
- 🧱 **Structured context**: prior injuries, position, injury category
- 🎯 **Fine-tuned BERT** with dual-head classification
- 🔍 **Live predictions** with **confidence scores**
- 📊 **Built-in feature importance + attention hooks**
- 🌐 **Streamlit UI** with dropdowns, metrics, and sample cases

---

## 🗂️ File Structure
```text
project/
├── src/
│   ├── predict_utils.py        # logic for prediction function
│   └── final_injury_model.pt   # fine-tuned dual-head transformer model (DistilBERT)
├── requirements.txt            # all dependencies (Torch, HF Transformers, Streamlit, etc.)
├── modeling_notebooks/         # experimentation, feature importance, attention
├── cleaned_data/               # cleaned dataset used for training
├── raw_data/                   # original source CSVs
└── README.md                   # this file
```

---

## ⚙️ Setup

1. **Install dependencies**

```bash
pip install -r requirements.txt
```
2. ****
```bash

```
---

## ⚙️ Model Overview

| **Component**          | **Description**                                           |
| ---------------------- | --------------------------------------------------------- |
| **Base Model**         | `distilbert-base-uncased`                                 |
| **Input**              | Injury description text + structured inputs               |
| **Structured Inputs**  | Prior injuries, position ID, injury type ID               |
| **Output Heads**       | `label_type_id`, `label_duration_id`                      |
| **Optimization**       | Multi-task cross-entropy loss                             |
| **Performance Boosts** | Attention score injection, feature dropout, class weights |

---

## 📈 Results Summary

| Metric              | Value   | Description                                                   |
|---------------------|---------|---------------------------------------------------------------|
| **Type Accuracy**   | 99.5%   | Nearly perfect prediction for general injury type            |
| **Duration Accuracy** | 65.0% | More challenging task due to overlap in medium/long classes  |
| **Macro F1 (Duration)** | ~0.64 | Balanced F1 across duration classes                          |
| **Most Confused Pair** | `long` vs `medium` | Long and medium often overlapped in symptoms and context |
| **Evaluation Set Size** | 200 samples | Held-out test subset from full dataset                     |
| **Unknown Labels Removed** | ✅ | Improved class balance and duration accuracy                |
| **Feature Importance** | moderate | Prior injuries most useful, attention least influential     |

---

## What I learned

Structured + Textual fusion drastically improves performance over text-only

Class balancing + weighted loss helped fix bias toward short injuries

Adding features like injury type, position, prior injuries sequentially allowed modular experimentation

Attention scores showed low influence, but modeling it validated model interpretability

---

## 💬 Sample Predictions

"torn ACL expected to miss rest of season"  
→ Type: **joint** (99%), Duration: **long** (91%)

"minor hamstring strain"  
→ Type: **muscle** (96%), Duration: **short** (87%)

"fractured tibia, placed on IL"  
→ Type: **bone** (98%), Duration: **long** (89%)

---

## Hugging Face Transformers & Datasets

PyTorch, Scikit-learn, and for all underlying tech

---

## Datasets
- Player_Info: [NBA Players stats since 1950](https://www.kaggle.com/datasets/drgilermo/nba-players-stats?select=player_data.csv)
- Player_Info:[NBA Players data (1950 to 2022)](https://www.kaggle.com/datasets/blitzapurv/nba-players-data-1950-to-2021?select=player_data.csv)
- Injury Info: [🏀 NBA Injury Stats (1951–2023)](https://www.kaggle.com/datasets/loganlauton/nba-injury-stats-1951-2023)

---

## 🧠 Try it Out Now
Enter a short injury description, and get:

✅ Predicted injury type

⏳ Estimated recovery time

📈 Confidence scores

✨ Fork this space and customize it to your league, team, or medical use case.
