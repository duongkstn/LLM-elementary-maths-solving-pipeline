# Zalo AI Challenge 2023 - Elementary Maths Solving
## A Solution of top-5 private leaderboard

### Problem
Problem Statement can be found at https://challenge.zalo.ai/portal/elementary-maths-solving

![Screenshot from 2023-12-22 09-20-05](https://github.com/duongkstn/LLM-elementary-maths-solving-pipeline/assets/25122601/ffdcba7c-5b5b-4b5f-83ba-ec24c42449e4)

### Overview
![pipeline](https://github.com/duongkstn/LLM-elementary-maths-solving-pipeline/assets/25122601/60557d49-77c3-4947-a040-2c994a1b45b0)
*Our inference pipeline*

Our contributions as follow: :heart_eyes:
- Creating rule-base algorithm to pass basic testcases
- Collecting and augmenting Vietnamese elementary mathematics from internet
- Training a LLM
- Appying RAG technique
- Implementing re-evaluation method for inference

### Details
#### 1. Rule-base algorithm

We were able to calculate and derive outcomes directly by using `regex` and `numexpr`to infer results without relying solely on LLM.

#### 2. Dataset


The given dataset contains approx. 1200 training examples, half of them include `explanation` field. So we decided to collect more multiple choice data from [VietJack](https://vietjack.me/). Furthermore, we augmented data by calling GPT-4 API to fill missing `explanation` samples.
We also created dataset programmatically for some types of math problem (including basic calculation). To diversify our dataset, we translated famous public datasets using Huggingface 🤗.
Note that our dataset not only contains samples in multiple choice format, but also in question-answering format.

#### 3. LLM

We conducted experiments using publicly available 7B and 13B models from `WizardLM`, `meta-math`, `FelixChao`, and `EleutherAI`. For efficient training, we employed `LoRA`, `deepspeed` and used hyperparameter tuning techniques to identify the optimal model configuration.

#### 4. RAG

We utilized RAG to enhance accuracy of LLM. Our model encountered frequent failures in certain problem types, and this is where RAG shined. We appended RAG knowledges into the input prompt to provide LLM with additional information, hence improving its reasoning abilities. In total, we had 10-20 knowledges and employed a simple keyword-based matching algorithm for retrieval.

#### 5. Re-evaluation

Although applying advanced techniques, we observed that LLM still encountered challenges in certain problems due to limitations in calculation abilities, despite their correct reasoning capabilities. To address this, we implemented a big loop where we re-evaluated calculation results using `numexpr` each time a equation appeared in output.
Note that, in order to reduce the complexity of our solution, only basic arithmetic equations would be considered.

### Authors

- [Mem 1](https://github.com/santapo)
- [Mem 2](https://github.com/BinhMinhs10)
- [Mem 3](https://github.com/duongkstn)


*Hope you guys love our solution !* :smiling_face_with_three_hearts: :smiling_face_with_three_hearts: :smiling_face_with_three_hearts:




