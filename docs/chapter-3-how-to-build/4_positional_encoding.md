# 4. Positional Encoding 

## 4.1 Absolute Positional Embedding (APE)

> [44] A. Vaswani, N. Shazeer, N. Parmar, J. Uszkoreit, L. Jones, A. N. Gomez, L. Kaiser, and I. Polosukhin, “Attention is all you need,” Advances in neural information processing systems, vol. 30, 2017.

Used in original Transformer model. Positional information added to input embedding at the bottom of both encoder and decoder stack. Main drawback being (1) restriction to a certain of tokens (2) fails to account for relative distances between tokens. 

## 4.2 Relative Positional Embeddings (RPE)

> [126] P. Shaw, J. Uszkoreit, and A. Vaswani, “Self-attention with relative position representations,” arXiv preprint arXiv:1803.02155, 2018.

Involve extending self-attention to consider pairwise link between input elements. Implemented at two levels: (1) additional components to the keys (2) sub-component of the value matrix. It looks at input as a fully-connected graph with labels and directed edges. 

## 4.3 Rotary Positional Embeddings (RoPE) 

It uses a rotational matrix to encode absolute position of words so it captures both absolute and relative positions. Useful features: flexible with sentence length, decrease in word dependency as relative distance increase, improve linear self-attention with relative position encoding. 


## 4.4 Relative Positional Bias

Developed to facilitate extrapolation during inference for sequence longer than those encountered in training. e.g. Attention with Linear Biases (ALiBi). 

> [128] O. Press, N. A. Smith, and M. Lewis, “Train short, test long: Attention with linear biases enables input length extrapolation,” arXiv preprint arXiv:2108.12409, 2021

