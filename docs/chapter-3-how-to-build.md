# How to build

![This figure shows different components of LLMs](images/LLM-training-process.png)

## 1. Architecture 

### 1.1 Transformer

> A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. Gomez, L. Kaiser, and I. Polosukhin, “Attention is all you need,” Advances in neural information processing systems, vol. 30, 2017.

The core mechanism is the (self-)attention mechanism, which can capture long-term contextrual information much more effectively using GPUs than the recurrence and convolusion mechanisms. Consists of an encoder(N = 6 identical Transformer layers, each layer consists of two sub-layers, a multi-head self-attention layer and a simple position wise fully connected feed-forward network) and a decoder (a stack of 6 identical layers, in addition to two layers in encoder, a third layer that performs multi-head attention over the output of encoder stack). 

Attention function can be described as mapping the query and a set of key-value pairs to a output - all vectors. The output is computed as a weighted sum of values, where the weight assigned to each value computed by a compatibility function. Instead of single attention with $d_{model}$ dimensional keys, values and queries, found beneficial to linearly project queries, keys and values h with different, learned linear projections to $d_k$, $d_k$, and $d_v$ dimensions. Position encoding is incorporated to fuse information about the position of the tokens. 

<span style="color: red;">need to understand position encoding and attention mechanism math by application</span>

### 1.2 Encoder Only 

Example: BERT. At each stage, atttention layers can access all words in the initial sentence. Great for tasks needs understanding of full sentence.  

### 1.3 Decoder Only

Example: GPT. At each stage, for any words, attention layer can only access words positioned before that in the sentence. Sometimes called auto-regressive models, best suited for text generation. 

> 现在所有模型都是 Decoder Only 吗？

### 1.4 Encoder Decoder 

Sometimes called sequence to sequence models. At each stage, attention layers of the encoder can access all the words in the initial sequence, and decoder only access words positioned before a given word in the input. Usually pretrained using the objective of encoder or decoder models. Best suited for tasks about generating new sentences conditioned on a given input, such as summarization, translation or answer question. 

> 有啥例子？

## 2. Data Cleaning 

### 2.1 Data Filtering

Aim to improve the quality of training data and effectiveness of trained LLMs. Common techniques: 

* Removing Noise: Eliminate irrelevant or noisy data. E.g. remove false information to avoid false response. Mainstream approaches: classifier-based and heuristic-based frameworks. 
* Handling Outliers: Identify and handle anomalies to prevent disproportionately influencing the model. 
* Addressing Imbalances: balance the distribution of classes or categories to avoid biases and ensure fair representation. Useful for responsible model training and evaluation. 
* Text preprocessing: cleaning and standardizing text data by removing stop words, punctuation, or other elements that may not contribute significantly to the model's learning 
* Dealing with Ambiguities: Resolve or exclude ambiguous or contradictory data that might confuse the model during training. Help produce reliable and definite answers.   

### 2.2 Deduplication

remove duplicate or repeated occurance of data. Duplicated data can introduce biases and reduce diversity --> overfitting. Existing works mainly reply on the overlap ratio of high-level features (e.g. n-grams overlap) between documents to detect duplicate samples. 


## 3. Tokenizations 

Out-of-vocabulary (OOV) is a problem in tokenization because tokenizer only knows words in dictionary. Below are three popular tokenizer: 

### 3.1 BytePairEncoding 

Originally a type of data compression algorithm that uses frequent patterns at byte level to compress the data. It tries to keep frequent words in their original form and break down onces that are not common. 

### 3.2 WordPieceEncoding 

Mainly used for BERT and Electra. At beginning of training takes all alphabet to make sure nothing is left as UNK (unknown) from training set. It then tries to maximize the likelihood of putting all the tokens in vocabulary based on their frequency. 

>  感觉跟 BPE 没啥区别，现在还有啥模型用这个？2025 Oct 主流方法是啥？

### 3.3 SentencePieceEncoding 

Two encoding methods above (BPE and WPE) assume words being separated by white-space as granted. SentencePieceEncoding tries to address the issue in some language words can be corrupted by many noisy elements.  

## 4. Positional Encoding 

### 4.1 Absolute Positional Embedding (APE)

> [44] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. Gomez, L. Kaiser, and I. Polosukhin, “Attention is all you need,” Advances in neural information processing systems, vol. 30, 2017.

Used in original Transformer model. Positional information added to input embedding at the bottom of both encoder and decoder stack. Main drawback being (1) restriction to a certain of tokens (2) fails to account for relative distances between tokens. 

### 4.2 Relative Positional Embeddings (RPE)

> [126] P. Shaw, J. Uszkoreit, and A. Vaswani, “Self-attention with relative position representations,” arXiv preprint arXiv:1803.02155, 2018.

Involve extending self-attention to consider pairwise link between input elements. Implemented at two levels: (1) additional components to the keys (2) sub-component of the value matrix. It looks at input as a fully-connected graph with labels and directed edges. 

### 4.3 Rotary Positional Embeddings (RoPE) 

It uses a rotational matrix to encode absolute position of words so it captures both absolute and relative positions. Useful features: flexible with sentence length, decrease in word dependency as relative distance increase, improve linear self-attention with relative position encoding. 


### 4.4 Relative Positional Bias

Developed to facilitate extrapolation during inference for sequence longer than those encountered in training. e.g. Attention with Linear Biases (ALiBi). 

> [128] O. Press, N. A. Smith, and M. Lewis, “Train short, test long: Attention with linear biases enables input length extrapolation,” arXiv preprint arXiv:2108.12409, 2021

## 5. Model Pre-training 

Different approaches used for pre-training, two most common ones include: (1) next token prediction (autoregressive) (2) masked language modeling

### 5.1 Autoregressive Language Modelling 

Given a sequence of $n$ tokens $x_1, \ldots, x_n$, model tries to predict next token $x_{n+1}$. Popular loss function is **log-likelihood of predicted tokens**: 

$$
\mathcal{L}*{\text{ALM}}(x) =
\sum*{i=1}^{N}
p(x_{i+1} \mid x_i, \ldots, x_{i+n-1})
\tag{1}
$$

Usually in decoder only models. 

### 5.2 Masked Language Modeling (MLM)

Mask some words in a sequence and train model to predict masked words based on context. Sometime called denoising autoencoding. If denote masked/corrupted samples in the sequence $x$, as $\tilde{x}$. The training objective is: 

$$
\mathcal{L}*{\text{MLM}}(x) =
\sum*{i=1}^{N}
p(\tilde{x}_i \mid x, \tilde{x})
\tag{2}
$$

### 5.3 Mixture of Experts (MoE)

Pre-train with less compute. Consists of two main elements: (1) **Sparse MoE layers** used instead of dense feed-forward network (FFN) layer and have a certain number of experts in which each is a neural network. (2) **A gate netowork or router** determine which tokens are sent to which expert.  

> [130] N. Shazeer, A. Mirhoseini, K. Maziarz, A. Davis, Q. Le, G. Hinton, and J. Dean, “Outrageously large neural networks: The sparsely-gated mixture-of-experts layer,” arXiv preprint arXiv:1701.06538, 2017.

## 6. Fine-tuning and Instruction Tuning 

### 6.1 Instruction Tuning 

> [133] S. Zhang, L. Dong, X. Li, S. Zhang, X. Sun, S. Wang, J. Li, R. Hu, T. Zhang, F. Wu, and G. Wang, “Instruction tuning for large language models: A survey,” 2023.

Align responses to the expectations human will have when providing instructions through prompts . 

## 7. Alignment 

### 7.1 RLHF (Reinforcement Learning from Human Feedback) and RLAIF (Reinforcement Learning from AI Feedback)

Use a reward model to learn alignment from feedback. Reward model can rate different outputs and score them according to alignment preferences. Reward model can give feedback to model output, then use this feedback to tune LLMs further. 

### 7.2 DPO (Direct Preference Optimization)

RLHF is often complex and unstable. DPO use a mapping between reward functions and optical policies to show this contrained reward maximization problem can be maximized with a single stage of policy training, essentially solving a classification problem on the human preference data. 

<span style="color: red;">I don't fully understand this section. Need further clarification and examples.</span>

### 7.3 GRPO (Group Relative Policy Optimization)

Method from DeepSeek.  

## 8. Decoding Strategies 

Decoding refer to process of text generation using pre-trained LLMs. Input prompt --> tokenizer --> token IDs --> predict --> logits --> convert to probability using softmax function. From here, different decoding strategies have been proposed. 

### 8.1 Greedy Search 

Take most probably token at each step as the next token in sequence, discarding all other potential options. Can miss out better sequences that might appear with less probability.  

### 8.2 Beam Search 

Consider next $N$ most likely tokens, where $N$ denotes number of beams. Repeat this process until a predefined maximum sequence length or end-of-sequence token. The sequence with highest overall score will be chosen as output. More computationally intensive, for beam size of 2 and maximum length of 5, needs to keep track of $2^5 = 32$ possible beams. 

### 8.3 Top-k Sampling 

Select token randomly from $k$ most likely options. 

For example, suppose have 6 tokens (A, B, C, D, E, F) and k=2, and P(A)=30%, P(B)=20%, P(C)=P(D)=P(E)=P(F)=12.5%. Token C, D, E, F are disregarded. The model output A 60% of time, B 40% of time. 

Randomness introduced via temperature, it affects probability of softmax function. Temperature simply consists of dividing input logits by temperature value: 

$$
softmax(x_i) = \frac{e^{x_i / T}}{\sum_j{e^{x_j / T}}}
$$

### 8.4 Top-p Sampling 

Slightly different from top-k, it choose a cutoff value p such that the sum of probabilities of selected token exceeds p. Add token to list until probability exceeds p. Number of token in p is not fixed, good for scenarios like top-k does no have significant mass. 

## 9. Cost-Effective Training/Inference/Adaptation/Compression

### 9.1 Optimized Training

* ZeRO (Zero Redundancy Optimizer): optimize memory and improve training speed. Low communication volume and high computational granularity. 
* RWKV (Receptance Weighted Key Value): Combine efficient parallelizable training of Transformer with RNN. Use a linear attention mechanism so formulate model as either Transformer or RNN. 

> B. Peng, E. Alcaide, Q. Anthony, A. Albalak, S. Arcadinho, H. Cao, X. Cheng, M. Chung, M. Grella, K. K. GV et al., “Rwkv: Reinventing rnns for the transformer era,” arXiv preprint arXiv:2305.13048, 2023.

### 9.2 Low Rank Adaption (LoRA) 

A popular technique to reduce number of trainable parameters. Approximate weights to low rank matrix. 

> E. J. Hu, Y. Shen, P. Wallis, Z. Allen-Zhu, Y. Li, S. Wang, L. Wang, and W. Chen, “Lora: Low-rank adaptation of large language models,” arXiv preprint arXiv:2106.09685, 2021.


### 9.3 Knowledge Distillation

Train smaller model by learning from larger models. Knowledge can be transferred by different form of learning: 

* response distillation: concern only outputs of teacher model and student model try to exactly or similarly perform as teacher  
* feature distillation: uses last layer and intermediate layers to create better inner representations of student model
* and API distillation: use api from provider to train smaller model

#### 9.4 Quantization

Reduce precision of weights to reduce size of model and make it faster. 