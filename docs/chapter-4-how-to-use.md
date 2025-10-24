# How to use LLMs 

LLM have limitations, so there are tools and techniques beyond LLM to fix them. Here are some limitations:  

* no memory 
* are probabilistic
* cannot actively access external information
* generally large 
* hallucinate 

## Current Techniques on how to mitigate limitations of LLM 

### no memory 

currently embed memory in prompt and use RAG.  

### are probabilistic

Fine tune or prompt engineering to improve stability. 

### cannot actively access external information

Agents using ReACT, function call and MCP to access external information. 

### generally large 

Run in cloud, run in better GPU or run with quantization (FP8, FP16) . Not many good ways to avoid this. Some research shows proper quantization does not affect model quality much. 

<span style="color: red;">need to find sources for techniques that reduce model size and maintain performance (quantization, pruning, distillation, etc.)</span>

### hallucinate 

Use prompt engineering, RAG or fine tune to reduce hallucination. More advanced models tend to hallucinate less but cannot eliminate completely. 

Two types of hallucination: 
(1) Intrinsic Hallucination: directly conflict with source material, introducing factual inaccuracies or logical inconsistency. 
(2) Extrinsic Hallucination: unverifiable against the source, encompassing speculative or unconfirmable elements 

## Prompt Engineering 

* Chain-of-Thoughts (CoT): Address reasoning deficiency by guiding model through essential reasoning steps. Make implicit reasoning process explicit. 

> J. Wei, X. Wang, D. Schuurmans, M. Bosma, b. ichter, F. Xia, E. Chi, Q. V. Le, and D. Zhou, “Chain-of-thought prompting elicits reasoning in large language models,” in Advances in Neural Information Processing Systems, S. Koyejo, S. Mohamed, A. Agarwal, D. Belgrave, K. Cho, and A. Oh, Eds., vol. 35. Curran Associates, Inc., 2022, pp. 24 824–24 837. [Online]. Available: https://proceedings.neurips.cc/paper files/paper/ 2022/file/9d5609613524ecf4f15af0f7b31abca4-Paper-Conference.pdf

* Tree-of-Thoughts (ToT): guide model to consider various alternative solutions or thought processes before converge on the most plausible one. 

* Self-Consistency: Generate multiple responses to the same query and choose the most accurate one based on human's thought. 

* Reflection: Prompt LLM to assess/revise its own output based on reasoning

> [160] N. Shinn, F. Cassano, E. Berman, A. Gopinath, K. Narasimhan, and S. Yao, “Reflexion: Language agents with verbal reinforcement learning,” 2023.

* Workflow and/or multi-agent: LLM follow a predefined workflow or interact with different prompted agents complete task towards a pre-set goal. 

* Automatic Prompt Engineering (APE): automatically generate, score, refine and iterate prompt towards a goal. E.g. **DsPy prompt optimizer**

> [163] Y. Zhou, A. I. Muresanu, Z. Han, K. Paster, S. Pitis, H. Chan, and J. Ba, “Large language models are human-level prompt engineers,” 2023.

## Retrieval, Augmentation, Generation (RAG)

Many techniques, mainly using vector databases and various database techniques like k-v pairs to achieve different effect. 


## Tools 

* ReACT: First proposed by LangChain. Allow model to use Observe, Reason, and Act to prompt itself to use tools. Unreliable but simple to use. 
* Function Calling: The model calls tool directly without using prompts and tokens. Requires re-training of model but more reliable. However, can call limited number of with more tools the model hallucinate more. Usually one round. 
* Model Context Protocal (MCP): The model can access a standardize set of tools and reason to call the correct one. More standardized and allow call multiple tools in multiple rounds. Can complete more complex task. Usually multiple rounds. 
* Agent 2 Agent (A2A): Allow LLM to interact with pre-defined agents, can compete more complex tasks. Ideally, the model may self assess and iterate towards a predefined goal and explore possible routes without human interference. 