# 🤗 Hugging Face — Learning Notes

## What is Hugging Face?

**Hugging Face** is an open-source AI/ML ecosystem that provides pre-trained models, datasets, libraries, and tools for building and using machine learning and generative AI applications.

Its **Transformers** library makes it easy to use models for tasks such as:

- NLP
- Text generation
- Sentiment analysis
- Translation
- Summarization
- Computer vision
- Speech and audio

---

## 1. Pre-trained Model

A **pre-trained model** is a model that has already been trained on a large dataset.

Instead of training a model from scratch, we can reuse the learned knowledge for our own task.

```text
Large Dataset
     ↓
Training
     ↓
Pre-trained Model
     ↓
Reuse / Fine-tune
```

**Example:** BERT, GPT-based models, vision models, etc.

---

## 2. Dataset

A **dataset** is a collection of data used to train, evaluate, or test a machine learning model.

Examples:

```text
Text → NLP
Images → Computer Vision
Audio → Speech
```

Hugging Face provides access to many datasets through its ecosystem.

---

## 3. Fine-Tuning

**Fine-tuning** means taking an already trained/pre-trained model and training it further on a specific dataset or task.

```text
Pre-trained Model
       ↓
Task-specific Dataset
       ↓
Fine-tuning
       ↓
Specialized Model
```

### Training from scratch vs Fine-tuning

```text
Training from scratch:
Random Model → Large Dataset → Training → Model

Fine-tuning:
Pre-trained Model → Specific Dataset → Further Training → Specialized Model
```

Fine-tuning is generally much less expensive than training a large model from scratch.

---

## 4. Token

A **token** is a unit of text processed by a language model.

A token can be:

- A complete word
- Part of a word
- Punctuation
- Another piece of text

Therefore:

> **1 token ≠ 1 word**

For example:

```text
"I love machine learning!"
          ↓
      Tokenizer
          ↓
   Tokens / Token IDs
          ↓
   Transformer Model
```

The exact number of tokens depends on the tokenizer.

### Token limits

If a model supports a certain number of tokens, that refers to the amount of **tokenized text**, not the number of words.

For example:

```text
max_new_tokens = 80
```

means the model can generate up to approximately **80 new tokens**, not 80 words.

---

## 5. Tokenizer

A **tokenizer** converts human-readable text into tokens and then into numerical token IDs that the model can process.

```text
"I love AI"
     ↓
Tokenizer
     ↓
Tokens
     ↓
Token IDs
     ↓
Model
```

Different models can use different tokenizers, so the same sentence can have different token counts with different models.

---

## 6. Pipeline

A **pipeline** is a sequence of processing steps used to take input data and produce an output.

In general ML:

```text
Input
  ↓
Preprocessing
  ↓
Model
  ↓
Postprocessing
  ↓
Output
```

Hugging Face provides a high-level `pipeline()` API that makes it easy to use pre-trained models without manually handling every step.

Example:

```python
from transformers import pipeline

classifier = pipeline("sentiment-analysis")

result = classifier("I love machine learning!")
print(result)
```

Possible output:

```text
POSITIVE
```

The Hugging Face pipeline handles steps such as tokenization, model inference, and output processing.

---

## 7. Inference

**Inference** is the process of using a trained model to make predictions or generate outputs on new data.

```text
Training
   ↓
Trained Model
   ↓
New Input
   ↓
Inference
   ↓
Prediction / Output
```

Example:

```text
"What is AI?"
      ↓
    LLM
      ↓
   Inference
      ↓
"AI is..."
```

### Simple difference

> **Training = teaching the model**

> **Inference = using the trained model**

Inference is a general machine learning concept, not something specific to Hugging Face.

---

## 8. LoRA

**LoRA (Low-Rank Adaptation)** is a parameter-efficient fine-tuning technique.

Instead of updating a large number of parameters in a pre-trained model, LoRA:

- Keeps the original model weights frozen
- Adds small trainable matrices/adapters
- Trains only those additional parameters

```text
Pre-trained Model
       ↓
Original Weights → Frozen
       ↓
LoRA Adapters → Trainable
       ↓
Fine-tuned Model
```

### Why use LoRA?

It can reduce:

- GPU memory requirements
- Training computation
- Training time
- Storage requirements

LoRA is a **fine-tuning technique**, not a model itself.

---

# 🔄 Overall Flow

The concepts learned so far can be connected like this:

```text
                 DATASET
                    │
                    ↓
              PRE-TRAINING
                    │
                    ↓
            PRE-TRAINED MODEL
                    │
           ┌────────┴────────┐
           │                 │
           ↓                 ↓
      Use directly       Fine-tuning
           │                 │
           │              LoRA / PEFT
           │                 │
           │                 ↓
           │          Specialized Model
           │                 │
           └────────┬────────┘
                    ↓
                 INPUT
                    ↓
                TOKENIZER
                    ↓
               TOKEN IDs
                    ↓
             TRANSFORMER
                    ↓
                INFERENCE
                    ↓
                 OUTPUT
```

---

# 🧠 Key Terms

| Concept | Meaning |
|---|---|
| **Hugging Face** | AI/ML ecosystem for models, datasets and tools |
| **Pre-trained Model** | Model already trained on data |
| **Dataset** | Collection of data used by ML systems |
| **Tokenizer** | Converts text into tokens/token IDs |
| **Token** | Basic text unit processed by an LLM |
| **Pipeline** | Simplifies the ML processing workflow |
| **Inference** | Using a trained model to produce an output |
| **Fine-tuning** | Further training a pre-trained model for a specific task |
| **LoRA** | Parameter-efficient fine-tuning technique |
| **Transformers** | Library for working with transformer-based models |

## Practical Learning

The next step is to download a small pre-trained model from Hugging Face and run inference locally.

```text
Hugging Face Model Hub
        ↓
Download Pre-trained Model
        ↓
Load Model + Tokenizer
        ↓
Give Input
        ↓
Inference
        ↓
Output
```
