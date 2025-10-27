# 5. Model Pre-training 

Different approaches used for pre-training, two most common ones include: (1) next token prediction (autoregressive) (2) masked language modeling

## 5.1 Autoregressive Language Modelling 

Given a sequence of $n$ tokens $x_1, \ldots, x_n$, model tries to predict next token $x_{n+1}$. Popular loss function is **log-likelihood of predicted tokens**: 

$$
\mathcal{L}_{\text{ALM}}(x) =
\sum_{i=1}^{N}
p(x_{i+1} \mid x_i, \ldots, x_{i+n-1})
\tag{1}
$$

Usually in decoder only models. 

## 5.2 Masked Language Modeling (MLM)

Mask some words in a sequence and train model to predict masked words based on context. Sometime called denoising autoencoding. If denote masked/corrupted samples in the sequence $x$, as $\tilde{x}$. The training objective is: 

$$
\mathcal{L}_{\text{MLM}}(x) =
\sum_{i=1}^{N}
p(\tilde{x}_i \mid x, \tilde{x})
\tag{2}
$$

## 5.3 Mixture of Experts (MoE)

Pre-train with less compute. Consists of two main elements: (1) **Sparse MoE layers** used instead of dense feed-forward network (FFN) layer and have a certain number of experts in which each is a neural network. (2) **A gate netowork or router** determine which tokens are sent to which expert.  

> [130] N. Shazeer, A. Mirhoseini, K. Maziarz, A. Davis, Q. Le, G. Hinton, and J. Dean, “Outrageously large neural networks: The sparsely-gated mixture-of-experts layer,” arXiv preprint arXiv:1701.06538, 2017.

