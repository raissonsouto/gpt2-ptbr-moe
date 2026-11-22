# GPT-2 PT-BR MoE

GPT-2 trained from scratch on Portuguese academic text, for the Large Language Models course of the Graduate Program in Computer Science (PPGCC) at the Federal University of Campina Grande (UFCG).

The central question is: **what does a Mixture of Experts (MoE) gain over a dense model at the same scale and with the same token budget?** Starting from the GPT-2 implemented in Sebastian Raschka's [*Build a Large Language Model (From Scratch)*](https://www.manning.com/books/build-a-large-language-model-from-scratch) ([code](https://github.com/rasbt/LLMs-from-scratch)), the project optimizes the training pipeline and compares the dense vanilla model against two MoE variants and one additional architecture change. Every model is trained for one epoch (~27M tokens) on the introductions of 23,026 UFCG academic works.

## Experiments

| Run | Model | Question |
| --- | --- | --- |
| 1 | Vanilla GPT-2 with optimized training (fp16 + GradScaler, FlashAttention, fused AdamW, `torch.compile`) | How much throughput and memory do the optimizations save? |
| 2 | MoE (8 experts, top-2) with the **same active parameters** per token as the vanilla model | Does MoE improve quality at the same cost per token? |
| 3 | MoE with the **same total parameters** as the vanilla model | Does MoE improve quality at the same model size? |
| 4 | One architecture change (to be defined) vs. vanilla | — |

All runs use the 16k BPE reference tokenizer, the same token budget, the same learning rate schedule and the same fixed seed.

## Base configuration

| Hyperparameter | Value |
| --- | --- |
| Layers | 4 |
| Attention heads | 4 |
| Embedding dimension | 256 |
| Context length | 256 |
| Vocabulary | 16,000 (reference tokenizer) |
| Parameters | ~11M (~7M with weight tying) |
| Training budget | 1 epoch, ~27M tokens |

See [`configs/base.yaml`](configs/base.yaml).

## Contents

| Path | Description |
| --- | --- |
| `configs/` | One configuration file per experiment. |
| `src/gpt2ptbr/` | Model, MoE layer, data loading and training loop. |
| `scripts/` | Entry points: training, benchmarking and `evaluate.py` (bits per byte on a text file). |
| `data/` | Corpus and reference tokenizer (not versioned, see [`data/README.md`](data/README.md)). |
| `logs/` | Versioned training logs. Every number in the paper comes from here. |
| `checkpoints/` | Model checkpoints (not versioned, SHA-256 hashes listed below). |
| `notebooks/` | Analysis: loss curves, expert utilization, generated samples. |
| `paper/` | Paper in SBC format. |

## Checkpoints

| Model | SHA-256 |
| --- | --- |
| Vanilla | — |
| MoE (same active params) | — |
| MoE (same total params) | — |
| Run 4 | — |
