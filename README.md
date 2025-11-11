# SCQA-BioBERT-BiGRU

Official source code and model weights for the paper:
**"Innovative Multi-Model Technique for Medical Subject Classification and Answer Prediction"**

This repository contains the full Jupyter Notebook and trained model weights required to reproduce the results presented in our revised manuscript (submission to *Systems and Soft Computing*).

## 📝 Overview

This project implements a multi-task learning framework for medical question answering, designed to simultaneously perform **Subject Classification** and **Answer Prediction**.

[cite_start]Our final proposed architecture, `SCQA-BioBERT-BiGRU`, is a hybrid model that leverages the domain-specific understanding of **BioBERT** [cite: 1605-1607] [cite_start]and the sequential modeling capabilities of a **BiGRU** layer [cite: 1149-1150].

## 🏆 Key Findings: Ablation Study

[cite_start]A core component of our research was a comprehensive 4-model ablation study to validate our architectural choices, respond to reviewer feedback (R1C8, R2C1, R2C2), and benchmark against advanced alternatives like the **Block-Recurrent Transformer (BRT)** [cite: 1672-1673].

Our findings (from a reproducible run with `seed=42`) show that our proposed `BioBERT + BiGRU` architecture achieves the best performance on both tasks, validating our central hypothesis that the addition of a sequential layer is the optimal enhancement, while further complexity (e.g., semantic features or BRT cells) hindered performance.

**Final Ablation Study Results (Test Set):**

| Model Configuration | Architecture | Subject F1-Score (Primary Task) | Answer Accuracy (Label-Based) |
|:---|:---|:---|:---|
| **Base Model** | `BioBERT + Attention` | 80.81% | 83.29% |
| **BiGRU Model (Ours)** | `BioBERT + BiGRU + Attn` | **81.13%** | **84.36%** |
| **BiGRU + Negation** | `BioBERT + BiGRU + Attn + Negation` | 80.61% | 84.06% |
| **BRT + Negation** | `BioBERT + BRT_Cell + Attn + Negation` | 79.89% | 83.45% |

---

## 🚀 Reproducibility Guide

Follow these steps precisely to reproduce the results reported in our paper.

### 1. Setup Environment

1.  **Clone Repository:**
    ```bash
    git clone [https://github.com/MohammadAnsariShiri/SCQA-BiOBERT-BiGRU.git](https://github.com/MohammadAnsariShiri/SCQA-BiOBERT-BiGRU.git)
    cd SCQA-BiOBERT-BiGRU
    ```

2.  **(CRITICAL) Download LFS Files:** This repository uses Git LFS for large model weights (`.bin` files). You **must** have Git LFS installed.
    ```bash
    # Install Git LFS (if not already installed)
    # git lfs install
    
    # Download the large model files from LFS
    git lfs pull
    ```

3.  **Install Dependencies:**
    Install the required Python libraries using the `requirements.txt` file (this includes the specific `transformers==4.36.2` version).
    ```bash
    pip install -r requirements.txt
    ```

### 2. Download Dataset

This repository does not host the MedMCQA dataset. You must download it from the official source.

1.  [cite_start]**Download:** Download the dataset from [https://github.com/MedMCQA/MedMCQA](https://github.com/MedMCQA/MedMCQA)[cite: 1583].
2.  **Create Folder:** Create a new folder named `data` in the root of this project.
3.  **Place Files:** Place the `train.json`, `dev.json`, and `test.json` files inside the `data/` folder.

The final directory structure **must** look like this:
