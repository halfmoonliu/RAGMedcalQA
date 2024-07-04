# RAG Faciliatated Medical Question Answering

## Summary

**This project aims to investigate the effectiveness of applying retrieval-augmented generation (RAG) on medical question answering**. **MedQuAD**, a **medical question answer dataset** containing more than **200 thousand question-answer pairs**, was used for the study. **With correctly paired question-document as input**, the **test accuracy and F-1 score achieved 74.49 and 81.41**, higher than accuracy and achieved using questions alone (63.71 and 77.01 respectively).  The **ROUGE-L and BLEU scores** using the correct question-document pair as input **were 12.66 and 13.72**, higher than using questions with retrieved documents and questions only as input. **The results show the potential of RAG to improve the performance of machine medical question answering**. Further research is needed to increase accuracy for clinical use.

## Code 

a. **Model training**: *1_ModelTraining_MedicalQA.ipynb* </br>
b. **Yes-No Answer Generation**: *2_YesNo_MedicalQuestions.ipynb* </br>
c. **Long Answer Generation**: *3_LongAnswer_MedicalQuestions.ipynb* </br>

## Background

Medical question answering can benefit caregivers by reducing workload and providing actionable insights. **The challenge of medical question answering is to generate accurate responses** using natural human languages. Recent advances in large language models (LLMs) have dramatically enhanced machine capacity to generate natural language. **With new findings being published on a regular basis**, the problem becomes even more challenging. **A document stating the newest findings might be proved wrong or irrelevant very soon**. LLMs are trained on a large amount of documents to generate the most likely (or probable) response. However, **the most probable answers to medical questions might be just wrong** and lead to fatal consequences. **The aim of this project is to explore the possibility of leveraging RAG to increase the performance of medical question answering**

 ## Dataset
**The dataset used for this study is PubMedQA** , a question-answering dataset **containing three subsets, PQA-L, PQA-U, and PQA-A, with 1, 61.2, and 211.3 thousand question-answer pairs respectively** [1]. The **questions and answers were obtained from PubMed**, one of the most popular biomedical research paper databases. For papers with a yes-no question as the title, the titles were selected directly as questions in PQA-L and PQA-U. In the **PQA-L (labeled) subset**, **human experts manually annotated the yes-no answer** (yes: 55.2%, no: 33.8%, maybe: 11.0%). In the PQA-U (unlabeled) subset, yes-no answers were not provided. For the other papers, the titles, which are statements, were ***converted into questions***, which formed the questions in the **PQA-A (artificial) subset**. For example, the title of the paper ”Spontaneous electrocardiogram alterations predict ventricular fibrillation in Brugada syndrome.” was transformed as “Do spontaneous electrocardiogram alterations predict ventricular fibrillation in Brugada syndrome?” and the yes-no answers were produced automatically (yes: 92.8 %, no: 7.2).


## Preprocessing

### Preprocessing

The PQA-A subset was **randomly split into training and validation dataset using a 9:1 ratio** for the yes-no answer prediction task. The PQA-L, the human annotated dataset, was used as the test dataset for both yes-no questions and long-answer generation. All textual data were tokenized using the pretrained BERT model [2] using Hugging Face’s transformers library (version 4.40.1).

### Document Retrieval

**All abstracts in the PQA-L subset were treated as candidate documents**. All the questions and candidate documents were represented using the [cls] token of the pretrained BERT model . **The question-document pair with the highest cosine similarity score was retrieved**.


### Yes-No Answer Generation

**The yes-no answer generation task was treated as a binary outcome prediction task.** Input text was represented with the BERT model’s [cls] token. The pretrained BERT model was applied, with a linear model on top of the attention layer. The final output passed through a tanh activation for the binary classification task. The model was fine-tuned on the PQA-A dataset after preprocessing with 3 epochs (learning rate: *1e-5*, .batch size: 8. The PQA-L dataset was used to test the performance of the model, using **three kinds of input (question only, question plus the retrieved most relevant paper abstract, question plus the actual paper abstract)**. Questions with “maybe”, instead of yes/no, as answers were excluded during the test phase. Overall accuracy and F1 score were used to assess the performance.

### Long Answer Generation

**For the long answer generation task, the GPT-2 [3] model was used to generate answers to questions using different inputs (question only, question plus the retrieved most relevant paper abstract, question plus the actual paper abstract)**. The **ROUGE** (Recall-Oriented Understudy for Gisting Evaluation)-L and **one-gram BLEU** (BiLingual Evaluation Understudy) **score were used to assess the quality of the generated response**. All the reported results were assessed using the held-out human annotated dataset (PQA-L).

## Results

<img width="700" alt="Table 1" src="https://github.com/halfmoonliu/RAGMedcalQA/assets/46064664/5b17aab9-c579-4e47-b32c-403f230dbd27">
<img width="700" alt="Table 2" src="https://github.com/halfmoonliu/RAGMedcalQA/assets/46064664/e0dccfb0-5e7d-4405-8297-065d5eb21011">

## References

1.	Jin, Qiao, et al. "Pubmedqa: A dataset for biomedical research question answering." *arXiv preprint* arXiv:1909.06146 (2019). </br>
2.	Devlin, Jacob, et al. "Bert: Pre-training of deep bidirectional transformers for language understanding." *arXiv preprint* arXiv:1810.04805 (2018). </br>
3.	Radford, Alec, et al. "Language models are unsupervised multitask learners." *OpenAI blog* 1.8 (2019): 9.  </br>

