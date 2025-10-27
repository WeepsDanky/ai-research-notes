# 2. Data Cleaning 

## 2.1 Data Filtering

Aim to improve the quality of training data and effectiveness of trained LLMs. Common techniques: 

* Removing Noise: Eliminate irrelevant or noisy data. E.g. remove false information to avoid false response. Mainstream approaches: classifier-based and heuristic-based frameworks. 
* Handling Outliers: Identify and handle anomalies to prevent disproportionately influencing the model. 
* Addressing Imbalances: balance the distribution of classes or categories to avoid biases and ensure fair representation. Useful for responsible model training and evaluation. 
* Text preprocessing: cleaning and standardizing text data by removing stop words, punctuation, or other elements that may not contribute significantly to the model's learning 
* Dealing with Ambiguities: Resolve or exclude ambiguous or contradictory data that might confuse the model during training. Help produce reliable and definite answers.  

## 2.2 Deduplication

remove duplicate or repeated occurance of data. Duplicated data can introduce biases and reduce diversity --> overfitting. Existing works mainly reply on the overlap ratio of high-level features (e.g. n-grams overlap) between documents to detect duplicate samples. 

