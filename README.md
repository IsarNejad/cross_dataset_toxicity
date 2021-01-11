Paper associated with this code repository:
 
Isar Nejadgholi and Svetlana Kiritchenko (2020) On Cross-Dataset Generalization in Automatic Detection of Online Abuse - WOAH2020 Shared Exploration: Bias and Unfairness in the Detection of Online Abuse 


Copyright (C) 2020 National Research Council Canada (NRC)

*****************************************************
Description: 

All the experiments can be run on Google-colab. 

__*topics.pdf*__: shows the 20 topics extracted from *Wiki*-dataset. Each topic is represented by 10 top words.  


__*wiki_lda_topics.pdf*__: trains an LDA topic model on the *Wiki*-dataset annotated for *Personal Attack*. Then uses this model to find the distribution of topics in two other datasets *Waseem*-dataset and *Founta*-dataset.

__*train_wiki_bert.ipynb*__: trains a BERT-based model with a subcategory of the *Wiki*-dataset to detect *Personal Attack*. Then applies this model on the *Waseem*-dataset and *Founta*-dataset and calculates accuracy per test class as described in the paper. 

For more information about the used datasets please refer to the paper. 

*****************************************************
Contact: 

isar.Nejadgholi@nrc-cnrc.gc.ca 

*****************************************************
Terms of Use: 

1. The code can be used freely for non-commercial research and educational purposes.

2. Do not redistribute the code. 

3. National Research Council Canada (NRC) disclaims any responsibility for the use of the codes listed here and does not provide technical support. 

***************************************