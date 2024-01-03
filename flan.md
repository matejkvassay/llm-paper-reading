[Back to title page](README.md)
# Finetuned Language Models Are Zero-Shot Learners
### Basic info
**Link:** https://arxiv.org/abs/2109.01652

**Submitted:** Sep 2021

**By:** Google Research

### Introduction
In this paper Google researchers explore whether LLM’s 0-shot inference abilities on previously unseen task can be improved by fine-tuning on language instruction templates, rather than directly supervised training on NLP tasks. 

### Data
To fine-tune models authors have prepared datasets based on 60 NLP tasks divided into 12 categories such as NLI, Closed-Book QA, Coreference resolution, etc. For each individual dataset 10 different instruction templates were created and automatically filled. This reformulated these supervised datasets into next-word prediction format suitable for decoder-only LLM. 

### Model 
Fine-tuning is performed on a 137B parameter autoregressive model LaMDA-PT (https://arxiv.org/pdf/2201.08239.pdf). This is the version not the LaMDA model not fine-tuned for dialog, pre-trained on ~2.5T BPE tokens with 32K vocabulary size. Resulting instruction fine-tuned model is called FLAN (Fine-Tuned Language Net). 

### Experiment setting 
To evaluate of usefulness of instruction fine-tuning for 0 shot inference on previously unseen tasks one NLP task category (i.e. all tasks belonging into the category) was separated as hold-out set for evaluation. From remaining categories training data was drawn. This process was repeated for multiple task categories. 

### Fine-tuning
In order to fine-tune on selected subset of clusters, from each dataset samples are drawn randomly using the proportional mixing scheme. This sampling scheme prevents over-fitting on NLP task with disproportionately larger number of samples, by setting an artificial limit on maximum number of examples in given task, used in computation of probability for drawing a sample from the given task. Multiple tasks are also packed into single sentence. These techniques are referenced from https://arxiv.org/pdf/1910.10683.pdf. 
Special EOS token was then used to separate instruction from the context. 

### Evaluation results
Authors have clearly proven that for significant portion of 0-shot inference tasks FLAN had outperformed 175B parameter GPT3 on almost all tasks.

Improvement is more significant for tasks like NLI which are formulated naturally like instructions, less significant on tasks like common sense reasoning where additional instruction words are more redundant. 
 
They have compared effect of instruction fine-tuning (IFT) with direct supervised fine-tuning (SFT) on 0-shot inference performance and proven that IFT performs better. 

Noteworthy result is study on multiple model sizes where instruction fine-tuning on model with 8B parameters or less actually decreased the performance on unseen 0-shot inference task. One suspected reason can be catastrophic forgetting caused by capacity of these smaller models being filled by the instruction tasks however it’s not evaluated.

### Conclusion
Authors of this paper have successfully proven their hypothesis that instruction fine-tuning is beneficial for 0-shot inference. 
--- 

[Back to title page](README.md)