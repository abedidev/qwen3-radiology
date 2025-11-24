# Clinical Multi-Label Disease Extraction from Abdominal Radiology Findings

This repository contains the implementation of a project on extracting multi-label disease findings from radiology reports using large language models.  

The project evaluates both zero-shot pretrained LLMs and fine-tuned LLMs using supervised clinical data.

The goal is to provide full transparency in preprocessing, modeling methodology, evaluation, and reproducibility.

---

## Repository Structure

root/
│
├── notebooks/
│ ├── 01_data_exploration.ipynb
│ ├── 02_pre_preprocessing.ipynb
│ ├── 03_training.ipynb
│ ├── 04_evaluation_finetuned_models.ipynb
│ ├── 05_evaluation_zero_shot.ipynb
│ └── 06_error_analysis.ipynb
│
├── train-statistics/
├── figures/
├── models/
├── data/
│
└── README.md
