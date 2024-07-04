# RAG Faciliatated Medical Question Answering

## Summary

**This project aims to investigate the effectiveness of applying retrieval-augmented generation (RAG) on medical question answering**. **MedQuAD**, a **medical question answer dataset** containing more than **200 thousand question-answer pairs**, was used for the study. **With correctly paired question-document as input**, the **test accuracy and F-1 score achieved 74.49 and 81.41**, higher than accuracy and achieved using questions alone (63.71 and 77.01 respectively).  The **ROUGE-L and BLEU scores** using the correct question-document pair as input **were 12.66 and 13.72**, higher than using questions with retrieved documents and questions only as input. **The results show the potential of RAG to improve the performance of machine medical question answering**. Further research is needed to increase accuracy for clinical use.

## Background

Medical question answering can benefit caregivers by reducing workload and providing actionable insights. **The challenge of medical question answering is to generate accurate responses** using natural human languages. Recent advances in large language models (LLMs) have dramatically enhanced machine capacity to generate natural language. **With new findings being published on a regular basis**, the problem becomes even more challenging. **A document stating the newest findings might be proved wrong or irrelevant very soon**. LLMs are trained on a large amount of documents to generate the most likely (or probable) response. However, **the most probable answers to medical questions might be just wrong** and lead to fatal consequences. **The aim of this project is to explore the possibility of leveraging RAG to increase the performance of medical question answering**

 ## Dataset
**The dataset used for this study is PubMedQA** , a question-answering dataset **containing three subsets, PQA-L, PQA-U, and PQA-A, with 1, 61.2, and 211.3 thousand question-answer pairs respectively** [1]. The **questions and answers were obtained from PubMed**, one of the most popular biomedical research paper databases. For papers with a yes-no question as the title, the titles were selected directly as questions in PQA-L and PQA-U. In the **PQA-L (labeled) subset**, **human experts manually annotated the yes-no answer** (yes: 55.2%, no: 33.8%, maybe: 11.0%). In the PQA-U (unlabeled) subset, yes-no answers were not provided. For the other papers, the titles, which are statements, were ***converted into questions***, which formed the questions in the **PQA-A (artificial) subset**. For example, the title of the paper ”Spontaneous electrocardiogram alterations predict ventricular fibrillation in Brugada syndrome.” was transformed as “Do spontaneous electrocardiogram alterations predict ventricular fibrillation in Brugada syndrome?” and the yes-no answers were produced automatically (yes: 92.8 %, no: 7.2).
