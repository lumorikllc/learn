---
layout: textbook
title: "Mastering Post-Training and RLHF for Large Language Models - Implement a supervised fine-tuning (SFT) pipeline"
date: 2025-09-14T06:54:09.444709
study_plan_url: "https://lumorikllc.github.io/learn/content/a23f2f35-2cd5-455f-b58b-fa1815dadfd1/8f68736b-d9ad-4a5c-84a4-09e70340f5f5/"
chapters: 9
author: "a23f2f35-2cd5-455f-b58b-fa1815dadfd1"
description: "AI-generated textbook by Lumorik"
---


## Chapter Overview
Fine-tuning a large language model on your specific data lets it specialize in tasks like domain-specific Q&A or customer support. A robust supervised fine-tuning (SFT) pipeline ensures data quality, efficient training, and reliable evaluation.

By the end of this chapter, learners should be able to:
- Describe the core components of an SFT pipeline for LLMs.
- Implement data preprocessing, tokenization, and training loops.
- Compute and interpret loss and evaluation metrics in SFT.

## Key Concepts & Definitions
**Supervised Fine-Tuning (SFT)**: Post-pretraining step that adjusts model parameters via labeled input–output pairs.  
**Pretraining**: Initial unsupervised training on massive text corpora to learn language representations.  
**Tokenization**: Splitting text into tokens (words, subwords) for model input.  
**Dataset Curation**: Collecting, cleaning, and formatting labeled examples for training.  
**Loss Function**: Mathematical measure (e.g., cross-entropy) of model prediction error.  
**Learning Rate**: Step size controlling parameter updates during optimization.  
**Batch Size**: Number of examples processed together in one forward/backward pass.  
**Perplexity**: Exponential of average negative log-likelihood, measuring how well a model predicts data.  
**Evaluation Metrics**: Quantitative measures (BLEU, ROUGE, perplexity) to judge model performance.

These concepts interlock: you curate and tokenize data, select a loss function, and train the model with a chosen learning rate and batch size. Evaluation metrics then guide further data or hyperparameter adjustments.

## Main Exposition

### 1. Pipeline Overview
An SFT pipeline has four stages:
1. **Data Curation & Preprocessing**  
2. **Tokenization & Encoding**  
3. **Training Loop & Optimization**  
4. **Evaluation & Iteration**  

Each stage feeds into the next, forming a repeatable workflow.

### 2. Data Curation & Preprocessing
- Gather labeled pairs \[(input, target)\].  
- Clean text: normalize whitespace, remove duplicates.  
- Format as JSONL or CSV.  
Example JSONL line:
```json
{"prompt": "Define polymorphism.", "completion": "Polymorphism allows objects to be treated as instances of their parent class."}
```
- Split into train/validation sets (e.g., 90/10).

### 3. Tokenization & Encoding
Use a pretrained tokenizer:
```python
from transformers import AutoTokenizer
tokenizer = AutoTokenizer.from_pretrained("gpt2")
def encode(example):
    return tokenizer(example["prompt"], example["completion"],
                     truncation=True, padding="max_length")
```
Encoding yields `input_ids` and `attention_mask` tensors.

### 4. Training Loop & Optimization
Define cross-entropy loss:
$$
\mathcal{L} = -\sum_{t=1}^T \log p_{\theta}(y_t \mid y_{<t}, x)
$$
where $x$ is the prompt, $y$ the target tokens.

Simple PyTorch loop:
```python
import torch
from torch.utils.data import DataLoader
from transformers import AutoModelForCausalLM, AdamW

model = AutoModelForCausalLM.from_pretrained("gpt2")
optimizer = AdamW(model.parameters(), lr=5e-5)
loader = DataLoader(encoded_dataset, batch_size=8, shuffle=True)

model.train()
for epoch in range(3):
    for batch in loader:
        outputs = model(**batch, labels=batch["input_ids"])
        loss = outputs.loss
        loss.backward()
        optimizer.step()
        optimizer.zero_grad()
```

### 5. Evaluation & Iteration
Compute **perplexity** on validation:
$$
\text{PPL} = \exp\Bigl(\tfrac{1}{N}\sum_{i=1}^N -\log p(x_i)\Bigr)
$$
Lower PPL indicates better predictions. Also run BLEU/ROUGE on generated completions to measure quality.

## Applications & Real-World Context

**Domain-Specific Chatbot**  
A healthcare provider fine-tunes an LLM on medical Q&A pairs. After curation of 10 K question–answer pairs and SFT, the model correctly handles patient queries on symptoms and treatments, reducing support workload.

**Legal Document Summarization**  
A law firm compiles 5 K case summaries. Through SFT, the LLM learns to produce concise summaries of new cases, improving lawyer efficiency and ensuring consistent style.

## Common Misconceptions & Pitfalls
1. *More Data Always Helps.*  
  Quality matters as much as quantity—noisy labels degrade performance.  
2. *Single Epoch Suffices.*  
  Under-training leads to high loss; monitor metrics across epochs.  
3. *Bigger Batch Size Is Always Better.*  
  Too large batches can harm generalization; balance memory and performance.  
4. *Perplexity Alone Measures Quality.*  
  Perplexity ignores factual correctness and style; supplement with BLEU/ROUGE.

## Worked Example Problem

**Problem:**  
You have 1 000 prompt–completion pairs for product descriptions.  
1. Describe how to split and format the data.  
2. Write pseudocode for tokenization and DataLoader creation.  
3. Compute the loss for a single example where the model predicts probabilities $[0.1,0.6,0.3]$ for the true token sequence.

**Solution:**  
1. Split 900 training, 100 validation. Save as JSONL.  
2. Pseudocode:
   ```python
   tokenizer = AutoTokenizer.from_pretrained("gpt2")
   def encode(pair):
       return tokenizer(pair["prompt"], pair["completion"], truncation=True, padding="max_length")
   train_ds = map(encode, train_pairs)
   loader = DataLoader(train_ds, batch_size=16, shuffle=True)
   ```
3. Loss per token: $-\log p = [-\log(0.1), -\log(0.6), -\log(0.3)]$. Sum ≈ $2.30 + 0.51 + 1.20 = 4.01$.

## Practice Exercises
Q1. Define the role of a learning rate in SFT.  
Q2. Explain why validation split matters.  
Q3. Show the formula for perplexity given token log-probabilities.  
Q4. In code, how do you pass `labels` to compute loss in `transformers`?  
Q5. List two advantages of using JSONL for dataset storage.

## Summary & Further Reading
- SFT refines pretrained LLMs on labeled data for specialization.  
- Data curation, tokenization, training, and evaluation form the pipeline.  
- Cross-entropy loss drives parameter updates via backpropagation.  
- Perplexity, BLEU, and ROUGE help quantify model performance.  
- Hyperparameters (learning rate, batch size, epochs) require tuning.  
- Monitor validation metrics to avoid overfitting.  
- Iterative refinement improves both data quality and model output.

Annotated Bibliography  
1. Radford et al., “Language Models are Few-Shot Learners” (2020) – Introduces GPT-3’s pretraining and fine-tuning.  
2. Wolf et al., “Hugging Face’s Transformers” (2020) – Comprehensive guide to tokenizer and model APIs.  
3. Rogers et al., “A Primer in BERTology” (2020) – Survey of downstream fine-tuning methods.  
4. Papineni et al., “BLEU: a Method for Automatic Evaluation” (2002) – Foundation of text generation evaluation metrics.

## Solutions
A1. Controls step size in gradient updates; too large diverges, too small slows learning.  
A2. Ensures unbiased performance estimates and overfitting detection.  
A3. $\displaystyle \text{PPL} = \exp\bigl(-\tfrac{1}{N}\sum \log p(x_i)\bigr)$.  
A4. Pass `labels=batch["input_ids"]` to the model call: `model(**batch, labels=batch["input_ids"])`.  
A5. JSONL stores one example per line, simplifies streaming, and is newline-delimited for easy parsing.
