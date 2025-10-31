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

Same formulation as the DeepSeepMath model. 

### Reward modelling

Reward is source of training signal, decides the optimization direction of RL. A rule based system mainly consists of: 
(1) Accuracy rewards: evaluates whether the response is correct e.g. for math problems, leetCode
(2) Format rewards: enforce model to put its thinking process between <think> and </think> tags

Do not apply the outcome or process neural reward in DeepSeek-R1-Zero because it may suffer reward hacking in large scale RL process. Retrain reward model needs additional training resources and complicates the pipeline. 

### Training template

A simple template to adhere to instructions. 

```markdown 
A conversation between User and Assistant. The user asks a question, and the Assistant solves it. The assistant first thinks about the reasoning process in the mind and then provides the user with the answer. The reasoning process and answer are enclosed within <think> </think> and <answer> </answer> tags, respectively, i.e., <think> reasoning process here </think> <answer> answer here </answer>. User: **prompt**. Assistant:
``` 

### Performance

Eval on pass@1 and cons@64 score. 

* AIME 2024 benchmark
* MATH-500
* GPQA Diamond 
* LiveCode Bench 
* CodeForces

## DeepSeep-R1: RL with cold start

Pipeline described in introduction. 

## Distillation

Only apply SFT and do not include an RL stage. 

## Experiment 

Evaluated on MMLU, MMLU-Redux, MMLU-Pro, C-Eval, CMMLU, IFEVal, FRAMES, GPQA Diamon, SimpleQA, C-SimpleAQ, SWE-Bench Verified, Aider, LiveCodeBench, Codeforces, Chinese National High School Mathematics Olympiad, AIME2024. 

Also evaled on open-ended tasks using LLM as judges AlpacaEval 2.0, Arena Hard. 

## Unsuccessful Attempts

### Process Reward Model (PRM) 

PRM is a reasonable method to guide the model toward better approaches for solving reasoning tasks. In practice, three main limitations: 
(1) Challenging to explicitly define a fine-grain step in general reasoning
(2) determine whether the current intermediate step is correct is a challenging
(3) inevitably lead to reward hacking and retrain reward model comlicates the pipeline

### Monte Carlo Tree Search (MCTS)

Inspired by AlphaGo, the method enhance test-time compute by breaking answers into smaller parts to allow the model to explore the solution space systematically. 

We prompt model to generate multiple tags that correspond to specific reasoning steps neccessary for the search. For training, first use collected prompts to find answers via MCTS guided by a pre-trained value model. Then use resulting QA pair to train both actor and value model. 

However, (1) unlike chess the search space is not well defined. Token generation's search space exponentially grow. If set maximum extension limits, easy to stuck in local optima. (2) Train a fine-grained value model is hard. So model limits iterative improve. 

