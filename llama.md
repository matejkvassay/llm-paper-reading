[Back to title page](README.md)
# LLaMA: Open and Efficient Foundation Language Models
### Basic info
**Link:** https://arxiv.org/abs/2302.13971

**Submitted:** Feb 2023

**By:** Meta AI

### Introduction
In LLaMA paper Meta AI brought series of 7B - 65B parameter LLMs trained on open source datasets. Main focus of the improvements is on fast/inexpensive inference. Therefore rather than increasing the model size in number of parameters researchers focused on improving performance by scaling up the dataset size while keeping the model reasonably small. 

Tradeoff between dataset and model size
LLaMA 7B and 13B param models were trained on 1T tokens. Chinchilla paper (https://arxiv.org/pdf/2203.15556.pdf) evaluated the optimal number of tokens for 10B model to be only ~205B tokens. If the same scaling laws applied to LLaMA training dataset and architecture it means the training budget is not used optimally however there will be better performance at no additional inference costs, which seems to be valuable for large-scale applications.

The same cannot be said about the main 65.2B parameter model, which is trained on 1.4T parameters. This one does follow the Chichilla recommendation - for 67B parameter model it’s 1.5T tokens evaluated as optimal. Unfortunately this makes interpreting the evaluation results little difficult in respect to how much is worth to invest into training budget over the Chinchilla recommendation.

### Training dataset
Training dataset is mixture of:
- CommonCrawl English
- C4
- GitHub code
- Gutenberg
- Books3
- StackExchange
- Wikipedia
- ArXiv

Some preprocessing steps are mentioned for each of them. Dataset is mostly composed of english data, not sure about the multi-lingual capabilities of these models.  

### Model architecture
The model is decoder-only (auto-regressive) architecture suitable for text generation. This is not mentioned in the paper but in the model docs: https://github.com/facebookresearch/llama/blob/main/MODEL_CARD.md.  Authors listed improvements over the legacy Transformer as:
- Pre-normalisation (such as GPT3, normalize input to TF sub-layers not output)
- SwiGLU activations 
- RoPE (Rotary positional embeddings, from GPTNeo)

### Training
Optimizer was AdamW. Optimization was done on multi-head attention by not storing attention weights and computing it for masked tokens. Authors also replaced PyTorch AutoGrad with their custom implementation saving expensive activation in combination with sequence parallelism. Training of 65B model took 21 days on 2048x A100 80GB GPUs.

### Evaluation
At the time of publication notable opponents of these models were PaLM (8B - 540B) and GPT-3 (175B).  The evaluation seems thorough and many tasks and benchmarks are used. Results are interesting especially in the mid-range model size, where for instance on 5-accuracy MMLU LLaMA 13B outperforms GPT-3 175B by 3 points on average. For some tasks 65B LLaMA model closely matches or even outperforms 540B PaLM model.

### Conclusion
Original LLaMA models achieved nice results and mostly contributed by making these models and information on architecture, training techniques and data sources used public.  

--- 

[Back to title page](README.md)