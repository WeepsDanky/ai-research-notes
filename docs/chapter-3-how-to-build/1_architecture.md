# 1. Architecture 

![This figure shows different components of LLMs](images/LLM-training-process.png)

## 1.1 Transformer

> A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. Gomez, L. Kaiser, and I. Polosukhin, “Attention is all you need,” Advances in neural information processing systems, vol. 30, 2017.

The core mechanism is the (self-)attention mechanism, which can capture long-term contextual information much more effectively using GPUs than the recurrence and convolution mechanisms. Consists of an encoder(N = 6 identical Transformer layers, each layer consists of two sub-layers, a multi-head self-attention layer and a simple position wise fully connected feed-forward network) and a decoder (a stack of 6 identical layers, in addition to two layers in encoder, a third layer that performs multi-head attention over the output of encoder stack). 

Attention function can be described as mapping the query and a set of key-value pairs to a output - all vectors. The output is computed as a weighted sum of values, where the weight assigned to each value computed by a compatibility function. Instead of single attention with $d_{model}$ dimensional keys, values and queries, found beneficial to linearly project queries, keys and values h with different, learned linear projections to $d_k$, $d_k$, and $d_v$ dimensions. Position encoding is incorporated to fuse information about the position of the tokens. 

<span style="color: red;">need to understand position encoding and attention mechanism math by application</span>

## 1.2 Encoder Only 

Example: BERT. At each stage, atttention layers can access all words in the initial sentence. Great for tasks needs understanding of full sentence.  

## 1.3 Decoder Only

Example: GPT. At each stage, for any words, attention layer can only access words positioned before that in the sentence. Sometimes called auto-regressive models, best suited for text generation. 

> 现在所有模型都是 Decoder Only 吗？

## 1.4 Encoder Decoder 

Sometimes called sequence to sequence models. At each stage, attention layers of the encoder can access all the words in the initial sequence, and decoder only access words positioned before a given word in the input. Usually pretrained using the objective of encoder or decoder models. Best suited for tasks about generating new sentences conditioned on a given input, such as summarization, translation or answer question. 

> 有啥例子？


## 1.5 RWKV (Receptance Weighted Key Value)

Combine efficient parallelizable training of Transformer with RNN. Use a linear attention mechanism so formulate model as either Transformer or RNN. 

> B. Peng, E. Alcaide, Q. Anthony, A. Albalak, S. Arcadinho, H. Cao, X. Cheng, M. Chung, M. Grella, K. K. GV et al., “Rwkv: Reinventing rnns for the transformer era,” arXiv preprint arXiv:2305.13048, 2023.

