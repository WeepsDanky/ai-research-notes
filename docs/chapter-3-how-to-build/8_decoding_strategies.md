# 8. Decoding Strategies 

Decoding refer to process of text generation using pre-trained LLMs. Input prompt --> tokenizer --> token IDs --> predict --> logits --> convert to probability using softmax function. From here, different decoding strategies have been proposed. 

## 8.1 Greedy Search 

Take most probably token at each step as the next token in sequence, discarding all other potential options. Can miss out better sequences that might appear with less probability.  

## 8.2 Beam Search 

Consider next $N$ most likely tokens, where $N$ denotes number of beams. Repeat this process until a predefined maximum sequence length or end-of-sequence token. The sequence with highest overall score will be chosen as output. More computationally intensive, for beam size of 2 and maximum length of 5, needs to keep track of $2^5 = 32$ possible beams. 

## 8.3 Top-k Sampling 

Select token randomly from $k$ most likely options. 

For example, suppose have 6 tokens (A, B, C, D, E, F) and k=2, and P(A)=30%, P(B)=20%, P(C)=P(D)=P(E)=P(F)=12.5%. Token C, D, E, F are disregarded. The model output A 60% of time, B 40% of time. 

Randomness introduced via temperature, it affects probability of softmax function. Temperature simply consists of dividing input logits by temperature value: 

$$
softmax(x_i) = \frac{e^{x_i / T}}{\sum_j{e^{x_j / T}}}
$$

## 8.4 Top-p Sampling 

Slightly different from top-k, it choose a cutoff value p such that the sum of probabilities of selected token exceeds p. Add token to list until probability exceeds p. Number of token in p is not fixed, good for scenarios like top-k does no have significant mass. 


