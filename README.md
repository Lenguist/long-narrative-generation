# Long-narrative-generation
This is a repository for research on long narrative generation. Specifically latest additions are dealing with developing automated metrics for long story evaluation.
Work performed for Language Generation and Summarization seminar at Columbia University.

The goal of this research was to develop automated metrics for evaluating coherence and premise relevance of AI generated stories of 1000+ words. For this purpose I leveraged data released by DOC as a gold standard human judgement with which to compare my metrics. The proposed metrics include heurstics, zero-shot and few-shot GPT3.5 answers, and longformer-classifier models trained on both synthetic data and human preferences.

We have also originally wanted to use reranker module from docstorygen but found it performed poorly in preliminary experimentation. You check that work in docstorygen folder in reranker file.

Additionally we tried to use reranker from docstorygen-v2, but it relies on openai logprobs which have been deprecated. You can check that out too in docstorygen-v2 folder.

All code in ipynb files have been written by me. Code in docstorygen and docstorygen-v2 is cloned from the original repositories.

NOTE: you need to put your openai api key in some places to run code. Usually it's very prominent in the first or second cell.

## Data
To download adapted human annotation preference data and synthetic training datasets for relevance and coherence follow this link:
[link]https://drive.google.com/file/d/1nwHM6UmgJKZY1XpI3AKAyfekEFE3Y8ty/view?usp=drive_link
The data was adapted from docpstorygen-v2 (link) dataset of generated short stories.
To generate your own synthetic data using synethtic-data.ipynb.

## Baselines
For baselines, open evaluate.ipynb and run the cells associated in Coherence/Heuristic, Coherece/GPT, Relevance/Heuristic and Relevance/GPT sections. Baselines do not need to be trained.

## Experiments
We propose two different longformer classifiers to evaluate coherence and relevance. One type is pairwise comparison, which is supplied two stories separated by [SEP] token and must output story1 or story2 as its prediction. The second type is a binary coherent/non-coherent classifier, which is supplied a single story and must output coherent or non-coherent as its prediction, the likelihood of coherence for each text is then used to produce pairwise preferences. We trained these models on two types of data: synthetic data generated using the generator we created, and human annotations. To train the models, go to the file train.ipynb. Originally training was performed in Colab but the notebook should be runnable locally as well. The notebook will push the saved models to huggingface hub.

In total we ended up training 4 models. Future work can explore more hyperparameter tuning and training on more data.

## Evaluation
Metric validation (aka model evaluation) is performed in evaluate.ipynb. The notebook will pull the models from huggingface hub. To evaluate your own model, you can upload it to huggingface hub and change the model name in the notebook.
