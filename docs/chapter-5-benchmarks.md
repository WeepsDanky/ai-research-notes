# Benchmarks

## Statistical Metrics

* Assessing text similarity, intrinsic hallucination

  * ROGUE [C.-Y. Lin, “ROUGE: A package for automatic evaluation of summaries,” in Text Summarization Branches Out. Barcelona, Spain: Association for Computational Linguistics, Jul. 2004, pp. 74–81. [Online]. Available: https://aclanthology.org/W04-1013]
  * BLEU [K. Papineni, S. Roukos, T. Ward, and W.-J. Zhu, “Bleu: a method for automatic evaluation of machine translation,” in Proceedings of the 40th Annual Meeting of the Association for Computational Linguistics, P. Isabelle, E. Charniak, and D. Lin, Eds. Philadelphia, Pennsylvania, USA: Association for Computational Linguistics, Jul. 2002, pp. 311318. [Online]. Available: https://aclanthology.org/P02-1040]
* Advanced Metrics:

  * PARENT [B. Dhingra, M. Faruqui, A. Parikh, M.-W. Chang, D. Das, and W. Cohen, “Handling divergent reference texts when evaluating table-to-text generation,” in Proceedings of the 57th Annual Meeting of the Association for Computational Linguistics, A. Korhonen, D. Traum, and L. Ma`rquez, Eds. Florence, Italy: Association for Computational Linguistics, Jul. 2019, pp. 4884–4895. [Online]. Available: https://aclanthology.org/P19-1483]
  * PARENT-T [Z. Wang, X. Wang, B. An, D. Yu, and C. Chen, “Towards faithful neural table-to-text generation with content-matching constraints,” in Proceedings of the 58th Annual Meeting of the Association for Computational Linguistics, D. Jurafsky, J. Chai, N. Schluter, and J. Tetreault, Eds. Online: Association for Computational Linguistics, Jul. 2020, pp. 1072–1086. [Online]. Available: https: //aclanthology.org/2020.acl-main.101]
  * Knowledge F1 [H. Song, W.-N. Zhang, J. Hu, and T. Liu, “Generating persona consistent dialogues by exploiting natural language inference,” Proceedings of the AAAI Conference on Artificial Intelligence, vol. 34, no. 05, pp. 8878–8885, Apr. 2020.]
* **Pass@k**: given a problem, different solutions as code are generated. Designed to test for correctness using different functionality tests. Measures the probability that at least one of the top-$k$ generated code samples for a problem passes all correctness tests.

$$
\text{Pass@}k :=
\mathbb{E}_{\text{Problems}}
\left[
1 -
\frac{
\binom{n - c}{k}
}{
\binom{n}{k}
}
\right]

$$

where:

* $\mathbb{E}_{\text{Problems}}[\cdot]$ — expectation over all problems in the benchmark dataset;
* $n$ — total number of code samples generated for a given problem;
* $c$ — number of those $n$ samples that are **correct** (i.e., pass all test cases);
* $k$ — number of code samples evaluated or “top-$k$” candidates considered for success;
* $\binom{n}{k}$ — binomial coefficient, i.e., the number of ways to choose $k$ items from $n$.

> 这个metric不好，正常来说人要求的应该是在一组里选的任何一个都是对的，而不是一组里只有一个对就行。

* Exact Match (EM): exact matches from (pre-defined) answers token by token 
$$ 
EM = \frac{M}{N}
$$

where $M$ is total number of correct answers and $N$ is number of questions. 

* Human Equivalence Score (HEQ): alternative to F1 score， evaluate how LLM answered compare with human's F1 score. 


## Model Based Metrics

* IE Based Metrics: Utilize Information Extraction models to simplify knowledge into relational tuples, then compare these with the source.
* QA Based Metrics: assess overlap between generated content and source [[152] O. Honovich, L. Choshen, R. Aharoni, E. Neeman, I. Szpektor, and O. Abend, “q2: Evaluating factual consistency in knowledgegrounded dialogues via question generation and question answering,” in Proceedings of the 2021 Conference on Empirical Methods in Natural Language Processing, M.-F. Moens, X. Huang, L. Specia, and S. W.-t. Yih, Eds. Online and Punta Cana, Dominican Republic: Association for Computational Linguistics, Nov. 2021, pp. 7856–7870. [Online]. Available: https://aclanthology.org/2021.emnlp-main.619]
* NLI Based Metric: Use natural language inference dataset to evaluate truthfulness .[[153] N. Dziri, H. Rashkin, T. Linzen, and D. Reitter, “Evaluating attribution in dialogue systems: The BEGIN benchmark,” Transactions of the Association for Computational Linguistics, vol. 10, pp. 1066–1083, 2022. [Online]. Available: https://aclanthology.org/2022.tacl-1.62]
* Faithfulness Classification Metrics: a refined assessment by creating task-specific datasets for a nuance evaluation [S. Santhanam, B. Hedayatnia, S. Gella, A. Padmakumar, S. Kim, Y. Liu, and D. Z. Hakkani-T ̈ur, “Rome was built in 1776: A case study on factual correctness in knowledge-grounded response generation,” ArXiv, vol. abs/2110.05456, 2021.]

## Human Judgement

* Scoring: human rate with predefined scale
* Comparative Analysis: compare generated content against baseline or ground-truth references

## English Math Benchmark 

* GSM8K 
  * K. Cobbe, V. Kosaraju, M. Bavarian, M. Chen, H. Jun, L. Kaiser, M. Plappert, J. Tworek, J. Hilton, R. Nakano, et al. Training verifiers to solve math word problems. arXiv preprint arXiv:2110.14168, 2021.
* MATH 
  * D. Hendrycks, C. Burns, S. Basart, A. Zou, M. Mazeika, D. Song, and J. Steinhardt. Measuring massive multitask language understanding. arXiv preprint arXiv:2009.03300, 2020. D. Hendrycks, C. Burns, S. Kadavath, A. Arora, S. Basart, E. Tang, D. Song, and J. Steinhardt. 
  * Measuring mathematical problem solving with the math dataset. arXiv preprint arXiv:2103.03874, 2021.
* SAT 
  * Z. Azerbayev, H. Schoelkopf, K. Paster, M. D. Santos, S. McAleer, A. Q. Jiang, J. Deng, S. Biderman, and S. Welleck. Llemma: An open language model for mathematics. arXiv preprint arXiv:2310.10631, 2023.
* OCW Courses 
  * A. Lewkowycz, A. Andreassen, D. Dohan, E. Dyer, H. Michalewski, V. V. Ramasesh, A. Slone, C. Anil, I. Schlag, T. Gutman-Solo, Y. Wu, B. Neyshabur, G. Gur-Ari, and V. Misra. Solving quantitative reasoning problems with language models. In S. Koyejo, S. Mohamed, A. Agarwal, D. Belgrave, K. Cho, and A. Oh, editors, Advances in Neural Information Processing Systems 35: Annual Conference on Neural Information Processing Systems 2022, NeurIPS 2022, New Orleans, LA, USA, November 28 - December 9, 2022, 2022b. URL http://papers.nips. cc/paper_files/paper/2022/hash/18abbeef8cfe9203fdf9053c9c4fe191-Abstr act-Conference.html.
  * A. Lewkowycz, A. Andreassen, D. Dohan, E. Dyer, H. Michalewski, V. Ramasesh, A. Slone, C. Anil, I. Schlag, T. Gutman-Solo, et al. Solving quantitative reasoning problems with language models. Advances in Neural Information Processing Systems, 35:3843–3857, 2022a.
* MMLU-STEM 
  * D. Hendrycks, C. Burns, S. Basart, A. Zou, M. Mazeika, D. Song, and J. Steinhardt. Measuring massive multitask language understanding. arXiv preprint arXiv:2009.03300, 2020.
  * D. Hendrycks, C. Burns, S. Kadavath, A. Arora, S. Basart, E. Tang, D. Song, and J. Steinhardt. Measuring mathematical problem solving with the math dataset. arXiv preprint arXiv:2103.03874, 2021.

## Chinese Math benchmarks 
* MGSM-zh 
  * F. Shi, M. Suzgun, M. Freitag, X. Wang, S. Srivats, S. Vosoughi, H. W. Chung, Y. Tay, S. Ruder, D. Zhou, D. Das, and J. Wei. Language models are multilingual chain-of-thought reasoners. In The Eleventh International Conference on Learning Representations, ICLR 2023, Kigali, Rwanda, May 1-5, 2023. OpenReview.net, 2023. URL https://openreview.net/pdf?id= fR3wGCk-IXp.
* CMATH 
  * J. Wei, X. Wang, D. Schuurmans, M. Bosma, B. Ichter, F. Xia, E. H. Chi, Q. V. Le, and D. Zhou. Chain-of-thought prompting elicits reasoning in large language models. In NeurIPS, 2022. URL http://papers.nips.cc/paper_files/paper/2022/hash/9d5609613524ecf 4f15af0f7b31abca4-Abstract-Conference.html.
  * T. Wei, J. Luan, W. Liu, S. Dong, and B. Wang. Cmath: Can your language model pass chinese elementary school math test?, 2023.
* Gaokao-MathCloze 
  * W. Zhong, R. Cui, Y. Guo, Y. Liang, S. Lu, Y. Wang, A. Saied, W. Chen, and N. Duan. AGIEval: A human-centric benchmark for evaluating foundation models. CoRR, abs/2304.06364, 2023. doi: 10.48550/arXiv.2304.06364. URL https://doi.org/10.48550/arXiv.2304.06364.
* Gaokao-MathQA 
  * W. Zhong, R. Cui, Y. Guo, Y. Liang, S. Lu, Y. Wang, A. Saied, W. Chen, and N. Duan. AGIEval: A human-centric benchmark for evaluating foundation models. CoRR, abs/2304.06364, 2023. doi: 10.48550/arXiv.2304.06364. URL https://doi.org/10.48550/arXiv.2304.06364.

## Natural Language Understanding, Reasoning and Code 

* Massive Multitask Language Understanding (MMLU)
  * D. Hendrycks, C. Burns, S. Basart, A. Zou, M. Mazeika, D. Song, and J. Steinhardt. Measuring massive multitask language understanding. arXiv preprint arXiv:2009.03300, 2020.
  * D. Hendrycks, C. Burns, S. Kadavath, A. Arora, S. Basart, E. Tang, D. Song, and J. Steinhardt. Measuring mathematical problem solving with the math dataset. arXiv preprint arXiv:2103.03874, 2021.
* BIG-Bench Hard (BBH)
  * F. Shi, M. Suzgun, M. Freitag, X. Wang, S. Srivats, S. Vosoughi, H. W. Chung, Y. Tay, S. Ruder, D. Zhou, D. Das, and J. Wei. Language models are multilingual chain-of-thought reasoners. In The Eleventh International Conference on Learning Representations, ICLR 2023, Kigali, Rwanda, May 1-5, 2023. OpenReview.net, 2023. URL https://openreview.net/pdf?id= fR3wGCk-IXp. 
  * M. Suzgun, N. Scales, N. Schärli, S. Gehrmann, Y. Tay, H. W. Chung, A. Chowdhery, Q. V. Le, E. H. Chi, D. Zhou, et al. Challenging big-bench tasks and whether chain-of-thought can solve them. arXiv preprint arXiv:2210.09261, 2022.

## Code Language Model 

* HumanEval 
  * W. Chen, X. Ma, X. Wang, and W. W. Cohen. Program of thoughts prompting: Disentangling computation from reasoning for numerical reasoning tasks. CoRR, abs/2211.12588, 2022. doi: 10.48550/ARXIV.2211.12588. URL https://doi.org/10.48550/arXiv.2211.12588.
  * P. Wang, L. Li, L. Chen, F. Song, B. Lin, Y. Cao, T. Liu, and Z. Sui. Making large language models better reasoners with alignment. arXiv preprint arXiv:2309.02144, 2023a.
  * M. Chen, J. Tworek, H. Jun, Q. Yuan, H. P. de Oliveira Pinto, J. Kaplan, H. Edwards, Y. Burda, N. Joseph, G. Brockman, A. Ray, R. Puri, G. Krueger, M. Petrov, H. Khlaaf, G. Sastry, P. Mishkin, B. Chan, S. Gray, N. Ryder, M. Pavlov, A. Power, L. Kaiser, M. Bavarian, C. Winter, P. Tillet, F. P. Such, D. Cummings, M. Plappert, F. Chantzis, E. Barnes, A. Herbert-Voss, W. H. Guss, A. Nichol, A. Paino, N. Tezak, J. Tang, I. Babuschkin, S. Balaji, S. Jain, W. Saunders, C. Hesse, A. N. Carr, J. Leike, J. Achiam, V. Misra, E. Morikawa, A. Radford, M. Knight, M. Brundage, M. Murati, K. Mayer, P. Welinder, B. McGrew, D. Amodei, S. McCandlish, I. Sutskever, and W. Zaremba. Evaluating large language models trained on code. CoRR, abs/2107.03374, 2021. URL https://arxiv.org/abs/2107.03374.
* MBPP
  * J. Austin, A. Odena, M. Nye, M. Bosma, H. Michalewski, D. Dohan, E. Jiang, C. Cai, M. Terry, Q. Le, et al. Program synthesis with large language models. arXiv preprint arXiv:2108.07732, 2021.