# Popular Datasets for LLMs 

Sure — here’s a clean **Markdown summary** of all datasets mentioned, grouped into the three main categories:

---

## 🧩 **A. Datasets for Basic Tasks**

*(Language modeling, understanding, generation)*

* **Natural Questions (NQ)** — Real Google search queries paired with Wikipedia pages; annotators mark long/short answers or null.
* **MMLU** — Multi-task benchmark over 57 subjects to assess zero/few-shot general knowledge and reasoning.
* **MBPP (Mostly Basic Python Problems)** — 974 short Python programming tasks with solutions and test cases for code generation.
* **HumanEval** — 164 hand-crafted programming problems with function signatures and unit tests; used to test code generation.
* **APPS** — 232K Python programs and 10K text-based problems with test cases; evaluates code generation.
* **WikiSQL** — 87K natural language–SQL query pairs from Wikipedia tables; tests text-to-SQL ability.
* **TriviaQA** — 650K question-answer-evidence triples authored by trivia enthusiasts, using Wikipedia and web sources.
* **RACE** — English reading-comprehension exams from Chinese students (middle/high school), ~100K questions.
* **SQuAD** — 100K question–answer pairs from Wikipedia passages; answers are text spans.
* **BoolQ** — Yes/no QA dataset with 16K questions and supporting paragraphs.
* **MultiRC** — Multi-sentence reading comprehension requiring reasoning across sentences; ~6K questions from 800 paragraphs.

---

## 🧠 **B. Datasets for Emergent Abilities**

*(In-context learning, reasoning, instruction following)*

* **GSM8K** — 8.5K grade-school math word problems requiring multi-step arithmetic reasoning.
* **MATH** — 12.5K high-school competition math problems with step-by-step LATEX solutions.
* **HellaSwag** — 70K multiple-choice commonsense reasoning questions derived from ActivityNet/WikiHow.
* **AI2 Reasoning Challenge (ARC)** — 7.8K science exam questions (Easy/Challenge sets) for commonsense reasoning.
* **PIQA** — Physical commonsense benchmark; choose between two plausible actions in daily scenarios.
* **SIQA (Social IQA)** — 38K multiple-choice questions testing social and emotional commonsense.
* **OpenBookQA (OBQA)** — 6K multiple-choice science questions requiring external commonsense facts.
* **TruthfulQA** — 817 questions across 38 categories (health, law, politics) testing factual truthfulness.
* **OPT-IML Bench** — 2K NLP tasks from 8 benchmarks (~18M examples) for instruction meta-learning evaluation.

---

## ⚙️ **C. Datasets for Augmented Abilities**

*(Using external knowledge, retrieval, or tools)*

* **HotpotQA** — 113K multi-hop reasoning questions from Wikipedia; requires combining two supporting paragraphs.
* **ToolQA** — QA benchmark testing an LLM’s ability to call and use external tools.
* **GPT4Tools** — Instruction dataset for tool usage generated from multimodal teacher models; includes train/validation/test splits with ~71K examples.

