# LLM from Scratch

Building Large Language Model components from scratch in PyTorch, following Sebastian Raschka's *Build a Large Language Model (From Scratch)*.

## Contents

| # | Topic | Notebook | Video |
|---|---|---|---|
| 02 | Attention, Transformer & GPT Pre-training | [Notebook](02-attention-transformer-gpt/02-attention-transformer-gpt.ipynb) | [Video](https://drive.google.com/file/d/1k_kR57DFEs87yhMOTcL72zO6CQWUtmKl/view?usp=sharing) |

## 02 — Attention, Transformer & GPT Pre-training

Implementation from scratch of the core components of a GPT-like LLM:

1. **Attention Mechanisms** — 4 variants: simple self-attention, trainable (Q/K/V), causal (masked + dropout), multi-head
2. **Transformer Block** — Pre-norm architecture with multi-head attention, feed-forward (GeLU), layer normalization and residual connections
3. **GPT Model** — Full GPT-2 Small architecture with HuggingFace weight loading and topology verification
4. **Memory Requirements** — Parameter counting with `.numel()` and weight tying analysis across GPT-2 family
5. **Portuguese Data Preparation** — Wikipedia PT corpus, BPE tokenization, sliding window dataset (max_length=256, stride=128)
6. **Pre-training** — 3 epochs with AdamW, qualitative evaluation showing transition from English to Portuguese generation

## Stack

- PyTorch
- tiktoken (BPE tokenizer)
- HuggingFace Transformers (weight loading)
- Plotly (loss curve visualization)

## References

- Raschka, S. *Build a Large Language Model (From Scratch)*, Manning, 2024
- Vaswani, A. et al. *Attention Is All You Need*, 2017
- Radford, A. et al. *Language Models are Unsupervised Multitask Learners* (GPT-2), 2019
