# Yoruba NER Robustness: Mixed Training for Missing Diacritics and Code-switch

This repository accompanies the paper **"Robust Yorùbá Named Entity Recognition through Simple Mixed Training"** by *Christian Adeoye Adebambo (2025)*.
It provides scripts and data processing code to reproduce experiments on the MasakhaNER 2.0 Yorùbá dataset using **XLM‑R** fine‑tuning and **LoRA** adaptation.

---

## Overview

Yorùbá text often omits tone marks and includes in‑line English (code‑switching), which can reduce model performance in downstream NLP tasks.
This project quantifies those effects for **Named Entity Recognition (NER)** and shows that a **simple 50–50 mixed training** setup, combining original and de‑diacritised text, restores robustness with minimal cost.

---

## Installation

Clone the repository:

```bash
git clone https://github.com/christianadebambo/yoruba-ner-robust.git
cd yoruba-ner-robust
```

Create a virtual environment and install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

---

## Usage

Open the notebook:

```bash
jupyter notebook yoruba_ner_robust.ipynb
```

The notebook runs end-to-end:
- Loads the **MasakhaNER 2.0 Yorùbá** dataset from Hugging Face  
- Creates extra evaluation splits:  
  - **No diacritics** (removes tone marks)  
  - **Code-switch** (inserts English filler words)  
- Tokenises text and aligns BIO tags using `xlm-roberta-base`  
- Trains three model setups:  
  1. **Full fine-tune** of `xlm-roberta-base`  
  2. **LoRA fine-tune** (parameter-efficient version)  
  3. **Mixed training** (original + no-diacritics data)  
- Evaluates all models across clean, no-diacritics, and code-switch test sets  
- Saves metrics and CSV outputs under `/kaggle/working/...`  
- Generates comparison plots for per-entity F1 scores  

> **Note:** The notebook paths are set up for Kaggle.  
> Adjust any file or output paths as needed if running locally.

## Example Results

| Model         | Clean F1 | No‑Diacritics F1 | Code‑switch F1 |
|----------------|-----------|------------------|----------------|
| XLM‑R Full     | 0.832     | 0.584            | 0.834          |
| XLM‑R LoRA     | 0.828     | 0.578            | 0.829          |
| XLM‑R Mixed    | 0.854     | 0.842            | 0.857          |

Figures generated in the paper are saved as:
- `fig_full_per_entity.png`
- `fig_mixed_per_entity.png`

---

## Citation

If you use this repository, please cite:

```bibtex
@article{adebambo2025yorubaner,
  title   = {Robust Yorùbá Named Entity Recognition through Simple Mixed Training},
  author  = {Adebambo, Christian Adeoye},
  year    = {2025}
}
```

---

## Licence

MIT License © 2025 Christian Adeoye Adebambo.
Based on public MasakhaNER 2.0 data under its original licence.

---

## Acknowledgements

Thanks to the **Masakhane NLP** community for the dataset and prior work on African NLP.
Special mention to **Iroro Orife**, **David Adelani**, and collaborators for foundational Yorùbá diacritic studies.