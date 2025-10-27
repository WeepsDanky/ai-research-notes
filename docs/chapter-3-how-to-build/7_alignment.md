# 7. Alignment 

## 7.1 RLHF (Reinforcement Learning from Human Feedback) and RLAIF (Reinforcement Learning from AI Feedback)

Use a reward model to learn alignment from feedback. Reward model can rate different outputs and score them according to alignment preferences. Reward model can give feedback to model output, then use this feedback to tune LLMs further. 

## 7.2 DPO (Direct Preference Optimization)

RLHF is often complex and unstable. DPO use a mapping between reward functions and optical policies to show this contrained reward maximization problem can be maximized with a single stage of policy training, essentially solving a classification problem on the human preference data. 

<span style="color: red;">I don't fully understand this section. Need further clarification and examples.</span>

## 7.3 GRPO (Group Relative Policy Optimization)

Method from DeepSeek.  


