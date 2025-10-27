# DeepSeekMath: Pushing the Limits of Mathematical Reasoning in Open Language Models

* Goal: mathematical reasoning
* Key contribution: (1) meticulous engineered data selection pipeline (2) GRPO
* Benchmarks: MMLU, BBH, GSM8K, MATH, CMATH 

## Method

(1) DeepSeek-Math Corpus, a large scale high quality pre-training corpus of 120B math tokens. Extraced from Common Crawl (CC) using a fastText-based classifier. Trained using OpenWebMath as positive examples. Then mine from CC and refined with human annotation. 

(2) DeepSeekMath-Base is initialized with DeepSeek-Coder-Base-v1.5 7B, noticed from code training model is better choice compared to a general LLM. Math training also improve model capability on MMLU and BBH benchmarks. 

(3) Apply mathematical tuning to DeepSeekMath-Nase with chain-of-thought, program-of-thought, and tool-integrated reasoning. Resulting model DeepSeekMath-Instruct 7B. 

> Z. Gou, Z. Shao, Y. Gong, Y. Shen, Y. Yang, M. Huang, N. Duan, and W. Chen. Tora: A toolintegrated reasoning agent for mathematical problem solving. CoRR, abs/2309.17452, 2023. doi: 10.48550/ARXIV.2309.17452. URL https://doi.org/10.48550/arXiv.2309.1745

(4) Group Relative Policy Optimization (GRPO), a variant Reinforcement Learning algorithm of Proximal Policy Optimization (PPO). GRPO estimate the baseline from group scores, significantly reducing training resources. 

## 3 Supervised Fine Tuning 

1. SFT Data Curation
   1. English mathematical database: GSM8K, MATH, Lila-OOD 
   2. Chinese mathematical database: Chinese K-12

## 4 Reinforcement Learning 

Reinforcement learning has been proven effective in further improving mathematical reasoning ability after Supervised-Fine-Tuning (SFT) stage. 

### From PPO to GRPO

PPO is an actor-critic RL algorithm that is widely used. It optimizes LLM by maximizing the following surrogate objective: 

![PPO surrogate objective](../images/PPO-equation.png)

where $\pi_{\theta}$ and $\pi_{\theta_{old}}$ are the current and old policy models, and $q, o$ are questions and outputs sampled from question dataset and old policy $\pi_{\theta_{old}}$, respectively. $\epsilon$ is a clipping-related hyper-parameter introduced in PPO for stabilizing training. $A_t$ is the advantage, computed by applying Generalized Advantage Estimation (GAE) based on the reward ${r_{\geq t}}$ and a learned value function $V_\psi$. 

In PPO, a value function needs to be trained alongside the policy model and to mitigate over-optimization of the reward-model. 

TBC...