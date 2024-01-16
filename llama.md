[Back to title page](README.md)
# LLaMA: Open and Efficient Foundation Language Models
### Basic info
**Link:** https://arxiv.org/abs/2302.13971

**Submitted:** Feb 2023

**By:** Meta AI

### Introduction
In this paper Meta AI introduced series of 7B - 65B parameter LLMs trained on open source datasets.

### Tradeoff between dataset and model size
By recommendation from Chinchilla paper (https://arxiv.org/pdf/2203.15556.pdf) the optimal pre-training dataset sizes are:
- ~205B tokens for 10B parameter model
- ~1.5T tokens for 67B parameter model

LLaMA is using following number of tokens for pre-training:
- ~1T tokens for 7B and 13B parameter models
- ~1.4T for 33B and 65B parameter models

The Chinchilla recommendation was followed for the 65B model but not for 7B and 13B. 
The intent was to create as good performing model as possible with reasonable inference costs, at expense of increased training budget.

### Training dataset
Training dataset is mixture of openly available datasets:
- CommonCrawl English
- C4
- GitHub code
- Gutenberg
- Books3
- StackExchange
- Wikipedia
- ArXiv

For each dataset different preprocessing was applied and BPE used for tokenization.

### Model architecture
The model is decoder-only (auto-regressive) architecture based on the original 2017 Transformer.
The main improvements over the legacy Transformer were:
- Pre-normalisation - normalize input to transformer sub-layers rather than output
- SwiGLU activations - trainable gated activation functions
- Rotary positional embeddings (RoPE) applied at each layer of the network

### Training
Optimization was done on multi-head attention by not storing nor computing attention weights for masked tokens. 

Authors have applied optimizations to speed up training:
- reduced number of activation re-computations by replacing PyTorch AutoGrad with optimized backward pass implementation
- used xformers multi-head attention which doesn't compute attention for masked tokens

Training of the largerst 65B model took 21 days on 2048x A100 80GB GPUs.

### Evaluation
LLaMA was compared to multiple available models such as Chinchilla (70B) PaLM (540B) and GPT-3 (175B).
Most evaluation focused on 0-shot and few-shot performance on various NLP benchmarks. 

Mid-sized LLaMA 13B outperformed GPT-3 175B by 3 points on average in the 5-shot MMLU accuracy.
The largest 65B LLaMA model was overall comparable to PaLM (540B) and Chinchilla (70B) models.

### Conclusion
Authors of this paper have proven that publicly available data can be used to train LLMs with performance matching commercial models trained on proprietary data. 

--- 

[Back to title page](README.md)