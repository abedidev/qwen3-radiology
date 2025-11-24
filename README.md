# Clinical Multi-Label Disease Extraction from Radiology Findings

This repository contains the implementation of a work on extracting multi-label disease findings from radiology reports using large language models.  
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
│   ├── 05-evaluation-fine-tuned-model.ipynb
│   ├── 06-hugging-face-upload.ipynb
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

This project uses a private dataset of abdominal radiology findings with multi-label disease outputs.

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

Implemented in:
```
01-evaluation-zero-shot.ipynb
02-fine-tuning-lora-dora.ipynb
03-fine-tuning-lora-dora-curriculum-learning.ipynb
04-fine-tuning-lora-dora-oversampling.ipynb
05-evaluation-fine-tuned-model.ipynb
06-hugging-face-upload.ipynb
```

Includes:
- Extracting the textual data from the CSV files  
- Integrating the text into prompts
- preparing the data in a format compatible with Hugging Face transformer models  


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

## 5. Inference and Zero-Shot Evaluation

### Zero-Shot Evaluation
```
01-evaluation-zero-shot.ipynb
```
### Fine-Tuned Model Evaluation
```
05-evaluation-fine-tuned-model.ipynb
```

### Hugging Face Model Upload
```
06-hugging-face-upload.ipynb
```

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
01-evaluation-zero-shot.ipynb
05-evaluation-fine-tuned-model.ipynb
```

Some Results:

| Model | Jaccard Score | Exact Match | Micro F1  | Macro F1 |
|-------|----------|----------|-------------|--------|
| Qwen3-4b Zero-shot | — | — | — | Figure 4 |
| Qwen3-8b Zero-shot | — | — | — | Figure 5 |
| Qwen3-8b LoRa | — | — | — | Default prompt |
| Qwen3-8b DoRa | — | — | — | Default prompt |
| Qwen3-8b LoRa | — | — | — | Default prompt |
| Qwen3-8b DoRa | — | — | — | Default prompt |

## 8. Reproducibility Statement

This repository follows MICCAI reproducibility guidelines.  
All processing, training, prompting, and evaluation steps are fully documented in notebooks.

## 9. Model Checkpoints (Hugging Face)

Fine-tuned models trained with Unsloth are available at:

```
[abedidev/qwen3-4b-unsloth-lora](https://huggingface.co/abedidev/qwen3-4b-unsloth-lora)
```

