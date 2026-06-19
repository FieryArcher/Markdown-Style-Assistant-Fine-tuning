# Markdown Style Assistant Fine-tuning

## Goal

The goal of this project is to fine-tune a public language model to answer in a structured markdown style.

## Model

Base model: TinyLlama/TinyLlama-1.1B-Chat-v1.0  
Fine-tuning method: LoRA / QLoRA  
Libraries: Hugging Face Transformers, PEFT, bitsandbytes, W&B

## Dataset

The dataset was created from an open instruction-response dataset and converted into a structured markdown response style.

Final format: JSONL with `instruction` and `response` fields.

## Data Processing

Data preparation included:

- removing empty examples
- removing duplicate instructions
- filtering low-quality or too short responses
- converting responses into markdown-style format
- splitting data into train and evaluation sets

## Training

Training was performed in Google Colab using a T4 GPU.

Training setup:

- LoRA / QLoRA fine-tuning
- adapter-based training
- 4-bit quantization
- training loss logging
- adapter saved instead of full model

## Evaluation

The base model and fine-tuned model were compared on several instruction prompts.

Evaluation includes:

- ROUGE score
- custom markdown style score
- qualitative comparison of generated answers

Results are available in:

- `reports/eval_results.json`
- `reports/examples_comparison.md`
- `reports/loss_curve.png`

## Results

The fine-tuned model became better at following the target markdown structure. It more consistently generated headings, bullet points, and conclusion sections. ROUGE only partially reflects this improvement, because the task is focused more on response style than exact text overlap.

## Files

- `data/train.jsonl` — training dataset
- `data/eval.jsonl` — evaluation dataset
- `outputs/markdown-style-adapter/` — saved LoRA adapter
- `reports/loss_curve.jpg` — training loss curve
- `reports/eval_results.json` — evaluation metrics
- `reports/examples_comparison.md` — base vs fine-tuned model examples

## How to Run

Install dependencies:

```bash
pip install -r requirements.txt
