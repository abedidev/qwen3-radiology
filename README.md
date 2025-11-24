# Clinical Multi-Label Disease Extraction from Abdominal Radiology Findings

This repository contains the official implementation of our work on extracting multi-label disease findings from abdominal radiology reports using large language models.
The project evaluates both zero-shot pretrained LLMs and fine-tuned LLMs using supervised clinical data.

This codebase follows the MICCAI Reproducibility Checklist and the Machine Learning Code Completeness Checklist for medical imaging and clinical AI research.
The goal is to provide full transparency in preprocessing, modeling methodology, evaluation, and reproducibility.

## Repository Structure

```
root/
│
├── notebooks/
│   ├── 01-evaluation-zero-shot.ipynb
│   ├── 02-fine-tuning-lora-dora.ipynb
│   ├── 03-fine-tuning-lora-dora-curriculum-learning.ipynb
│   ├── 04-fine-tuning-lora-dora-oversampling.ipynb
│   ├── 05-evaluation-fine-tuned.ipynb
├── inference-results.xlsx
│
├── train-statistics/
├── figures/
├── models/
├── data/
│
└── README.md
```

## 1. Environment and Requirements

### Operating System
- Ubuntu 22.04 or 24.04
- Python 3.10 or newer

### Hardware
- NVIDIA GPU recommended (e.g., RTX 3080 Ti, A100, or T4)

### Python Dependencies
Dependencies are listed in:

```
requirements.txt
```

Environment setup instructions are provided directly inside the notebooks.

## 2. Dataset

This project uses a dataset of abdominal radiology findings paired with gold-standard multi-label disease annotations.

### Dataset fields
- case_id
- input_finding (clinical text)
- output_disease (comma-separated disease labels)

### Private data note
If the dataset cannot be shared due to PHI restrictions:
- Users can run the entire pipeline by providing data in the same column structure.
- All necessary data preparation and preprocessing logic is included in the notebooks.

## 3. Preprocessing

Implemented in:

```
02_preprocessing.ipynb
```

Includes:
- Label normalization
- Vocabulary construction
- Text normalization
- Dataset splitting
- Tokenization preparation
- Statistical analysis of disease frequency, number of diseases per sample, and input text length

Generated statistics are saved in:

```
train-statistics/
```

## 4. Training

All fine-tuning is performed through:

```
03_training.ipynb
```

Includes:
- Loading pretrained LLMs
- Configuring PEFT methods (LoRA, DoRA, etc.)
- Hyperparameters
- Logging
- Saving fine-tuned checkpoints

The system prompt shown in Figure 4 is used as the default prompt during fine-tuning.

## 5. Inference and Zero-Shot Evaluation

### Fine-tuned Model Evaluation
```
04_evaluation_finetuned_models.ipynb
```

Includes:
- Running predictions
- Postprocessing
- Computing metrics
- Saving results

### Zero-shot Pretrained Evaluation
```
05_evaluation_zero_shot.ipynb
```

Uses both system prompts shown in Figure 4 and Figure 5.

## 6. Evaluation Metrics

Metrics include:
- Micro-F1
- Macro-F1
- Precision
- Recall
- Exact match
- Jaccard
- Per-disease metrics
- Error analysis by disease count, label co-occurrence, false positives, and false negatives

## 7. Results

Final metrics appear in:

```
04_evaluation_finetuned_models.ipynb
05_evaluation_zero_shot.ipynb
```

Example table:

| Model | Micro-F1 | Macro-F1 | Exact Match | Notes |
|-------|----------|-----------|-------------|--------|
| Zero-shot (Prompt A) | — | — | — | Figure 4 prompt |
| Zero-shot (Prompt B) | — | — | — | Figure 5 prompt |
| Fine-tuned LLM | — | — | — | Default: Figure 4 prompt |

## 8. Reproducibility Statement

This repository adheres to MICCAI reproducibility guidelines, providing full details for:
- Preprocessing
- Dataset statistics
- Training configuration
- Evaluation methodology
- Prompts used
- Notebook-based workflow

Reproducibility for private datasets is supported through complete transparency in each step, user-supplied datasets, and optional checkpoint sharing.

## 9. Model Checkpoints

Model weights, if provided, should be placed in:

```
models/
```

Include tokenizer files, adapter weights, and configuration metadata.

## 10. Acknowledgements

We acknowledge reproducibility frameworks from the MICCAI community and thank collaborators for their support.

## 11. License

Include your preferred license here.
