[Back to title page](README.md)
# Chain-of-Thought Prompting Elicits Reasoning in Large Language Models
### Basic info
**Link:** https://arxiv.org/abs/2201.11903

**Submitted:** Jan 2022

**By:** Google Research, Brain Team

### Introduction
In this paper authors propose a prompting technique called "Chain of Thought" aimed to solve more
complex language tasks such as arithmetic, symbolic and common sense reasoning. 

These tasks can typically be decomposed into a sequence of individual simpler reasoning steps leading to an answer. 
In prior work this was exploited by preparation of labeled datasets containing tasks decomposed to these individual 
steps, followed by fine-tuning language models capable of solving them. 

The Chain of Thought is based on the same decomposition idea. However rather than laboriously
prepare large amount of data for supervised fine-tuning, just small number of examples containing reasoning steps 
are provided to LLM as context in a few shot inference setting. 

### Data and prompt templates
For each task small number of few-shot examples are prepared manually by taking the original (task, answer) pair,
inserting new CoT passage in between them. 

#### Example of Question + CoT + Answer
**Question:** Is the following sentence plausible? "Kyle Palmieri was called for slashing."

**Chain of Thought**
Kyle Palmieri is a hockey player. Being called for slashing is part of hockey.

**Answer**
The answer is yes.

### Evaluation 

#### Experiment setup
CoT prompting is evaluated on multiple benchmarks for each of 3 reasoning types:
- Arithmetic - mostly math world problems e.g. elementary and grade school level
- Common sense - questions about the world, sports, inferring dates, etc.
- Symbolic - only 2 toy tasks - last letter of word concatenation and coin flip 

Evaluated models were done on varying model sizes:
  - GPT-3 (InstructGPT, 300M - 175B params)
  - LaMDA (422M  -137B params) 
  - PaLM (8B - 540B params) 
  - UL, 20B params
  - Codex (OpenAI model, size unknown)

#### Experiment results 
In evaluation it was shown that CoT often either comes close to the supervised state-of-the-art or human performance
and even surpasses it in some cases. CoT clearly outperformed standard few-shot prompting with (question, answer) pairs.

Interesting is that ability to benefit from CoT prompting was observerd only in models
with >100B paramters showing it's an emergent property of LLMs. Smaller models have produced realistic-looking chain 
of thoughts however not logically coherent. 

The more complicated the problem is to reason the more improvement was observed. For trivial tasks
the performance using CoT was even decreased since the chain of reasoning is redundant information. 

Authors also evaluate robustness of CoT in multiple aspects:
- Multiple annotators without ML background were creating prompts - the performance was always above standard prompting however it did introduce fluctuation in performance caused by quality of the prompt.
- Varying number of examples in few-shot context showed that usually 6-8 examples is optimal and increasing the number more didn't improve the performance.
- Varying permutation of order of examples in the provided context didn't cause significant variations in the performance.
- Some robustness against providing few shot examples from different distribution was also shown although only for the same task.

### Conclusion

In this paper Google researchers have demonstrated that Chain of Thought prompting is effective way how to solve complex reasoning tasks
which for people require multiple steps of thinking to arrive to an answer. 
They have proven that ability successfully mimic reasoning steps from small number of examples is an emerging property of LLMs.

--- 

[Back to title page](README.md)