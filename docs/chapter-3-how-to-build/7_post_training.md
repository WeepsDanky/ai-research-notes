# 7. Post-training 

## 6.1 Instruction Tuning 

> [133] S. Zhang, L. Dong, X. Li, S. Zhang, X. Sun, S. Wang, J. Li, R. Hu, T. Zhang, F. Wu, and G. Wang, “Instruction tuning for large language models: A survey,” 2023.

Align responses to the expectations human will have when providing instructions through prompts . 


## Rejection Sampling Fine-Tuning (RFT) 

> Z. Yuan, H. Yuan, C. Tan, W. Wang, S. Huang, and F. Huang. Rrhf: Rank responses to align language models with human feedback without tears. arXiv preprint arXiv:2304.05302, 2023b.
> Z. Yuan, H. Yuan, C. Li, G. Dong, C. Tan, and C. Zhou. Scaling relationship on learning mathematical reasoning with large language models. arXiv preprint arXiv:2308.01825, 2023a.

## 7.1 Reinforcement Learning 

> A. Kumar, V. Zhuang, R. Agarwal, Y. Su, J. D. Co-Reyes, A. Singh, K. Baumli, S. Iqbal, C. Bishop, R. Roelofs, et al. Training language models to self-correct via reinforcement learning. arXiv preprint arXiv:2409.12917, 2024.
> L. Ouyang, J. Wu, X. Jiang, D. Almeida, C. Wainwright, P. Mishkin, C. Zhang, S. Agarwal, K. Slama, A. Ray, et al. Training language models to follow instructions with human feedback. Advances in Neural Information Processing Systems, 35:27730–27744, 2022.

RLHF (Reinforcement Learning from Human Feedback) and RLAIF (Reinforcement Learning from AI Feedback). 

Use a reward model to learn alignment from feedback. Reward model can rate different outputs and score them according to alignment preferences. Reward model can give feedback to model output, then use this feedback to tune LLMs further. 

## 7.2 DPO (Direct Preference Optimization)

> R. Rafailov, A. Sharma, E. Mitchell, S. Ermon, C. D. Manning, and C. Finn. Direct preference optimization: Your language model is secretly a reward model. 2023.

RLHF is often complex and unstable. DPO use a mapping between reward functions and optical policies to show this contrained reward maximization problem can be maximized with a single stage of policy training, essentially solving a classification problem on the human preference data. 

<span style="color: red;">I don't fully understand this section. Need further clarification and examples.</span>

## 7.3 PPO (Proximal Policy Optimization)

An actor-critic RL algorithm that is widely used. Improved on Trust Region Policy Optimization (TRPO). 

> J. Schulman, F. Wolski, P. Dhariwal, A. Radford, and O. Klimov. Proximal policy optimization algorithms. arXiv preprint arXiv:1707.06347, 2017.
> J. Schulman. Approximating kl divergence, 2020. URL http://joschu.net/blog/kl-app rox.html.
> J. Schulman, P. Moritz, S. Levine, M. Jordan, and P. Abbeel. High-dimensional continuous control using generalized advantage estimation. arXiv preprint arXiv:1506.02438, 2015.

## 7.3 GRPO (Group Relative Policy Optimization)

> Z. Shao, P. Wang, Q. Zhu, R. Xu, J. Song, M. Zhang, Y. Li, Y. Wu, and D. Guo. Deepseekmath: Pushing the limits of mathematical reasoning in open language models. arXiv preprint arXiv:2402.03300, 2024.
> P. Wang, L. Li, Z. Shao, R. Xu, D. Dai, Y. Li, D. Chen, Y. Wu, and Z. Sui. Math-shepherd: A labelfree step-by-step verifier for llms in mathematical reasoning. arXiv preprint arXiv:2312.08935, 2023.

Method from DeepSeek.  


## Process-based reward models 

> H. Lightman, V. Kosaraju, Y. Burda, H. Edwards, B. Baker, T. Lee, J. Leike, J. Schulman, I. Sutskever, and K. Cobbe. Let’s verify step by step. arXiv preprint arXiv:2305.20050, 2023.

## Search Algorithms 

Monte Carlo Tree Search and Beam Search

> X. Feng, Z. Wan, M. Wen, S. M. McAleer, Y. Wen, W. Zhang, and J. Wang. Alphazero-like tree-search can guide large language model decoding and training, 2024. URL https: //arxiv.org/abs/2309.17179.
> H. Xin, Z. Z. Ren, J. Song, Z. Shao, W. Zhao, H. Wang, B. Liu, L. Zhang, X. Lu, Q. Du, W. Gao, Q. Zhu, D. Yang, Z. Gou, Z. F. Wu, F. Luo, and C. Ruan. Deepseek-prover-v1.5: Harnessing proof assistant feedback for reinforcement learning and monte-carlo tree search, 2024. URL https://arxiv.org/abs/2408.08152.