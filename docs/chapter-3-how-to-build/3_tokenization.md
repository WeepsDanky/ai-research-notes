# 3. Tokenizations 

Out-of-vocabulary (OOV) is a problem in tokenization because tokenizer only knows words in dictionary. Below are three popular tokenizer: 

## 3.1 BytePairEncoding 

Originally a type of data compression algorithm that uses frequent patterns at byte level to compress the data. It tries to keep frequent words in their original form and break down onces that are not common. 

## 3.2 WordPieceEncoding 

Mainly used for BERT and Electra. At beginning of training takes all alphabet to make sure nothing is left as UNK (unknown) from training set. It then tries to maximize the likelihood of putting all the tokens in vocabulary based on their frequency. 

>  感觉跟 BPE 没啥区别，现在还有啥模型用这个？2025 Oct 主流方法是啥？

## 3.3 SentencePieceEncoding 

Two encoding methods above (BPE and WPE) assume words being separated by white-space as granted. SentencePieceEncoding tries to address the issue in some language words can be corrupted by many noisy elements.  


