# Clinical Multi-Label Disease Extraction from Abdominal Radiology Findings

This repository contains the official implementation of our work on extracting multi-label disease findings from abdominal radiology reports using large language models.  
The project evaluates both zero-shot pretrained LLMs and fine-tuned LLMs using supervised clinical data.

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
│
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
- NVIDIA GPU recommended (RTX 3080 Ti, A100, T4)

### Python / Notebook Dependencies
All required packages for running this project in Google Colab are included and documented inside the notebooks.  
No standalone requirements.txt file is provided.

## 2. Dataset

This project uses a private dataset of abdominal radiology findings with expert-annotated multi-label disease outputs.

### Dataset Files
- train.csv – training set  
- test.csv – test set  

Both files contain the following fields:

- case_id  
- input_finding  
- output_disease  

### Private Data Note
As the dataset contains protected clinical data, it cannot be shared.  
Users can reproduce the pipeline by supplying their own dataset using the same structure.  
All preprocessing and preparation steps are included in the notebooks.

## 3. Preprocessing

Preprocessing steps are implemented across all notebooks used for training and evaluation:

```
01-evaluation-zero-shot.ipynb
02-fine-tuning-lora-dora.ipynb
03-fine-tuning-lora-dora-curriculum-learning.ipynb
04-fine-tuning-lora-dora-oversampling.ipynb
05-evaluation-fine-tuned.ipynb
```

Includes:
- Label normalization  
- Vocabulary construction  
- Text normalization  
- Dataset splitting  
- Tokenization setup  
- Statistical analysis (disease frequency, number of diseases per sample, input text length)

Generated statistics are stored in:

```
train-statistics/
```

## 4. Training

Fine-tuning is performed through:

```
02-fine-tuning-lora-dora.ipynb
03-fine-tuning-lora-dora-curriculum-learning.ipynb
04-fine-tuning-lora-dora-oversampling.ipynb
```

Includes:
- Loading pretrained LLMs  
- LoRA/DoRA PEFT configuration  
- Hyperparameters  
- Logging  
- Saving checkpoints  

The system prompt shown in Figure 4 is the default during fine-tuning.

## 5. Inference and Zero-Shot Evaluation

### Zero-Shot Evaluation
```
01-evaluation-zero-shot.ipynb
```
Uses both prompts shown in Figure 4 and Figure 5.

### Fine-Tuned Model Evaluation
```
05-evaluation-fine-tuned.ipynb
```

Includes:
- Running predictions  
- Postprocessing  
- Computing metrics  
- Exporting results  

## 6. Evaluation Metrics

- Micro-F1  
- Macro-F1  
- Precision  
- Recall  
- Exact match  
- Jaccard  
- Per-disease metrics  
- Error analysis (disease count, co-occurrence, FP/FN)

## 7. Results

Final results appear in:

```
05-evaluation-fine-tuned.ipynb
01-evaluation-zero-shot.ipynb
```

Example table:

| Model | Micro-F1 | Macro-F1 | Exact Match | Notes |
|-------|----------|----------|-------------|--------|
| Zero-shot (Prompt A) | — | — | — | Figure 4 |
| Zero-shot (Prompt B) | — | — | — | Figure 5 |
| Fine-tuned | — | — | — | Default prompt |

## 8. Reproducibility Statement

This repository follows MICCAI reproducibility guidelines.  
All processing, training, prompting, and evaluation steps are fully documented in notebooks.

## 9. Model Checkpoints

Place model files in:

```
models/
```

## 10. Acknowledgements

We acknowledge reproducibility guidelines from the MICCAI community.

## 11. License

Insert your chosen license here.
