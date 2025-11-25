# Fine-tuning Large Language Models for Disease Diagnosis 
Using Qwen3 Large Language Model with Parameter-Efficient Fine-Tuning

This repository provides an implementation and demonstration of using Qwen3 large language models for multi-label disease classification from free-text radiology findings. It covers the full workflow, beginning with preprocessing and prompt construction, followed by zero-shot evaluation and fine-tuning with LoRA and DoRA, and concluding with inference, comprehensive performance analysis, and uploading the resulting models to Hugging Face.

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
├── inference-results-raw.xlsx
├── inference-results-metrics.xlsx
│
└── README.md
```

## 1. Environment and Requirements

### Runtime Environment
This project is designed to run entirely in **Google Colab**, using the default Python and CUDA versions provided by the Colab runtime.

### Hardware
A GPU runtime is recommended for fine-tuning and evaluation  
(for example T4, V100, or A100 available in Colab).

### Python / Notebook Dependencies
All required packages are installed directly within the notebooks, and each notebook specifies its own dependencies. A separate `requirements.txt` file is therefore not included.

## 2. Dataset

This project uses a dataset of abdominal radiology findings with multi-label disease outputs that cannot be publicly released.

### Dataset Files
- `train.csv` – training set  
- `test.csv` – test set  

Both files contain the following fields:
- `case_id`  
- `input_finding`  
- `output_disease`

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
- Preparing the data in a format compatible with Hugging Face transformer models  

## 4. Training

Fine-tuning is performed through Unsloth:

![Unsloth Qwen-3 performance chart](figures/unsloth-qwen3.avif)


```
02-fine-tuning-lora-dora.ipynb
03-fine-tuning-lora-dora-curriculum-learning.ipynb
04-fine-tuning-lora-dora-oversampling.ipynb
```

Includes:
- Loading pretrained LLMs  
- LoRA and DoRA PEFT configuration  
- Applying curriculum learning strategies  
- Applying oversampling strategies for class imbalance  
- Hyperparameter configuration  
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

Final results were generated using:

```
01-evaluation-zero-shot.ipynb
05-evaluation-fine-tuned-model.ipynb
```

and appear in:

```
inference-results-raw.xlsx
inference-results-metrics.xlsx
```

including the raw inferences made by the models along with ground-truth values, as well as the values of different evaluation metrics.

### Some Results

| Model    | Setting   | Jaccard | Exact | Micro F1 | Macro F1 |
|----------|-----------|---------|-------|----------|----------|
| Qwen3-4B | Zero-shot | 0.2174  | 0.044 | 0.2956   | 0.0967   |
| Qwen3-8B | Zero-shot | 0.2157  | 0.044 | 0.2920   | 0.0831   |
| Qwen3-4B | LoRA      | 0.6034  | 0.3523| 0.6804   | 0.2630   |
| Qwen3-4B | DoRA      | 0.6122  | 0.3601| 0.6821   | 0.2830   |
| Qwen3-8B | LoRA      | 0.5988  | 0.3394| 0.6767   | 0.2711   |
| Qwen3-8B | DoRA      | 0.6209  | 0.3653| 0.6985   | 0.3104   |


## 8. Reproducibility Statement

All processing, training, prompting, and evaluation steps are fully documented in notebooks.

## 9. Model Checkpoints (Hugging Face)

Two of the fine-tuned models trained with Unsloth are available at:

abedidev/qwen3-4b-unsloth-lora
[abedidev/qwen3-4b-unsloth-lora](https://huggingface.co/abedidev/qwen3-4b-unsloth-lora)

abedidev/qwen3-8b-unsloth-dora
[abedidev/qwen3-8b-unsloth-dora](https://huggingface.co/abedidev/qwen3-8b-unsloth-dora)

## 10. License

This project is licensed under the **Apache License 2.0** - see the [LICENSE](LICENSE) file for details.

