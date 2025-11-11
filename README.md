# SCQA-BioBERT-BiGRU: A Hybrid Model for Medical QA

Official source code and model weights for the paper: 
**"Innovative Multi-Model Technique for Medical Subject Classification and Answer Prediction"**

This repository contains the Jupyter Notebook, analysis scripts, and final model weights required to reproduce the results presented in our manuscript.

## Overview

This project implements a multi-task learning framework for medical question answering, designed to simultaneously perform **Subject Classification** and **Answer Prediction**.

Our final proposed architecture, `SCQA-BioBERT-BiGRU`, is a hybrid model that leverages the domain-specific understanding of **BioBERT** [cite: 1605-1607] [cite_start]and the sequential modeling capabilities of a **BiGRU** layer. The model is enhanced with an attention mechanism to aggregate sequential features and Focal Loss to address class imbalance.

## Key Findings: Ablation Study

A core component of our research was a comprehensive 4-model ablation study to determine the optimal architecture. We compared four distinct configurations on the MedMCQA dataset using a fixed random seed (`seed=42`) for full reproducibility.

[cite_start]Our findings (presented in **Table 2** of the paper) confirm our central hypothesis: the hybrid **`BioBERT + BiGRU`** architecture provides the optimal performance on *both* tasks. Further complexity, such as additional semantic features (e.g., negation detection) or alternative recurrent layers (e.g., BRT), was found to hinder performance.

**Final Ablation Study Results (Test Set):**

| Model Configuration | Architecture | Subject F1-Score (Primary Task) | Answer Accuracy (Label-Based) |
|:---|:---|:---|:---|
| **Base Model** | `BioBERT + Attention` | 80.81% | 83.29% |
| **BiGRU Model (Ours)** | `BioBERT + BiGRU + Attn` | **81.13%** | **84.36%** |
| **BiGRU + Negation** | `BioBERT + BiGRU + Attn + Negation` | 80.61% | 84.06% |
| **BRT Model** | `BioBERT + BRT_Cell + Attn + Negation` | 79.89% | 83.45% |

---

## Reproducibility Guide

Follow these steps precisely to reproduce the results reported in our paper.

### 1. Environment Setup

1.  **Clone Repository:**
    ```bash
    git clone [https://github.com/MohammadAnsariShiri/SCQA-BiOBERT-BiGRU.git](https://github.com/MohammadAnsariShiri/SCQA-BiOBERT-BiGRU.git)
    cd SCQA-BiOBERT-BiGRU
    ```

2.  **(CRITICAL) Download Model Weights (LFS):**
    This repository uses Git LFS for large model weights (`.bin` files). You **must** have Git LFS installed.
    ```bash
    # Install Git LFS (if not already installed)
    # git lfs install
    
    # Download the large model files from LFS
    git lfs pull
    ```

3.  **Install Dependencies:**
    Install the required Python libraries using the `requirements.txt` file (this includes the specific `transformers==4.36.2` version required).
    ```bash
    pip install -r requirements.txt
    ```

### 2. Dataset Setup

This repository does not host the MedMCQA dataset due to its size and licensing. You must download it from the official source.

1.  [cite_start]**Download:** Download the dataset from [https://github.com/MedMCQA/MedMCQA](https://github.com/MedMCQA/MedMCQA) [cite: 2031-2032].
2.  **Create Folder:** Create a new folder named `data` in the root of this project.
3.  **Place Files:** Place the `train.json`, `dev.json`, and `test.json` files inside the `data/` folder.

The final directory structure **must** look like this:

SCQA-BioBERT-BiGRU/
├── data/
│   ├── train.json
│   ├── dev.json
│   └── test.json
├── model_outputs/
│   ├── Base_Model_BioBERT_Attention/
│   │   └── best_model_state.bin
│   ├── BiGRU_Model_No_Feature/
│   │   └── best_model_state.bin
│   └── ...
├── SCQA-BioBERT-BiGRU.ipynb
├── README.md
├── requirements.txt
└── LICENSE
 

### 3. How to Run

The `SCQA-BioBERT-BiGRU.ipynb` notebook contains all code.

**Option A: Verify All Results (Recommended - 5 minutes)**

To verify all tables and figures in the paper (Ablation Study, Per-Class reports, etc.) using our pre-trained model weights:

1.  Open `SCQA-BioBERT-BiGRU.ipynb`.
2.  Run all cells from the top (`# Imports`) down to `# Final Test Set Evaluation Functions`.
3.  **SKIP** the cell `# Run Ablation Study Experiments` (this cell is for training and takes 10+ hours).
4.  Run the **final cell** (`# --- 22. Run Final Evaluation on all 4 Models ---`).

This final cell will load our pre-trained weights from the `model_outputs/` folder and reproduce all metrics reported in the paper.

**Option B: Full Retraining (10+ hours)**

To retrain all four models from scratch, run all cells in the notebook from top to bottom. This will fully reproduce the results thanks to the fixed random seed (`set_seed(42)`).

---

## Citation

If you find this work useful in your research, please cite our paper:

**Manuscript Title:**
"Innovative Multi-Model Technique for Medical Subject Classification and Answer Prediction"

**BibTeX (placeholder):**
```bibtex
@article{AnsariShiri2025,
  title   = {Innovative Multi-Model Technique for Medical Subject Classification and Answer Prediction},
  author  = {Ansari Shiri, Mohammad, et al.},
  journal = {Submitted to Systems and Soft Computing},
  year    = {2025}
}
