# DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning

* Goal: Explore LLMs' reasoning capability without supervised data, self evolution through pure RL process
* method: 
  * DeepSeek-R1-Zero: use DeepSeek-V3-Base and GRPO as RL framework; 
  * DeepSeek-R1: use thousands cold-start data and multi-stage training. (1) Finetune DeepSeek-V3-Base with cold start data. (2) Perform reasoning-oriented RL like R1-zero (3) Create new SFT dataset. When near RL convergence, use data of rejection sampling on the RL checkpoint and supervised data (CoT) from DeepSeek V3 in specific domains. (4) an additional RL process for the checkpoint taking into account prompts from all scenarios. 
  * > “RL self-evolution” + “self-generated supervision loop”. 通过纯 RL 产生推理能力（R1-Zero），再用这些 RL 产生的好样本反向监督微调模型（R1），最后再 RL 一次完成闭环。
  * Distillation from DeepSeek-R1 to smaller dense models. Distillation from DeepSeek-R1 outperform applying RL on smaller dense models. Reasoning pattern discovered by large base model are crucial for improving reasoning. 
* Benchmarks: 
  * Reasoning
    * Math: Pass@1 on AIME 2024, MATH-500
    * Code competition: Elo rating on Codeforces 
    * Engineering: 
  * Knowledge:
    * education: MMLU, MMLU-Pro, GPQA Diamond 
    * factual: SimpleQA
  * Others: AlpacaEval 2.0, ArenaHard
  * Long context benchmark, creative writing, general question answering, editing, summarization etc. 


## Approach

### Group Relative Policy Optimization (GRPO)

To be continued... 