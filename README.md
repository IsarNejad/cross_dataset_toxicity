# A pruned version of the Wiki-toxicity dataset

This repository presents the code and data discussed in the following publication:
 
Isar Nejadgholi and Svetlana Kiritchenko (2020) On Cross-Dataset Generalization in Automatic Detection of Online Abuse - WOAH2020 Shared Exploration: Bias and Unfairness in the Detection of Online Abuse (also availabel at https://arxiv.org/abs/2010.07414)


Copyright (C) 2020 National Research Council Canada (NRC)

*****************************************************
This work presents a pruned version of the [*Wiki*-dataset labeled for toxicity](https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Toxicity/4563973). We showed that 54% of the training samples belong to topic numbers 3, 4, 5, 6, 10, 11, 13, 15, 17, 18, 19, which are mostly negative (benign) examples concerning Wikipedia-specific topics and have little impact on the performance of the toxicity classifier. These examples can be removed to obtain a pruned version of this dataset for faster training procedures. 

##  Code to generate the pruned training set:

```python
import pandas as pd
import re

comments = pd.read_csv('toxicity_annotated_comments.tsv', sep = '\t', index_col = 0)  #from https://figshare.com/articles/dataset/Wikipedia_Talk_Labels_Toxicity/4563973
annotations = pd.read_csv('toxicity_annotations.tsv',  sep = '\t')
# join labels and comments
comments['toxicity'] = annotations.groupby('rev_id')['toxicity'].mean() > 0.5

# remove newline and tab tokens
comments['comment'] = comments['comment'].apply(lambda x: x.replace("NEWLINE_TOKEN", " "))
comments['comment'] = comments['comment'].apply(lambda x: x.replace("TAB_TOKEN", " "))
comments['comment'] = comments['comment'].apply(lambda x:re.sub(r'[^A-Za-z0-9 ]+', ' ', x).lower())

wiki_topics = pd.read_csv('wiki_toxicity_topics.csv', index_col=[0]) #from this repo

data = comments.merge(wiki_topics, on='rev_id')  #merge the two datasets

#pruned Wiki-toxic 
topic_categories={1:[0,1],
                  2:[2,7,8,9,12,14,16],
                  3:[3,4,5,6,10,11,13,15,17,18,19]}


toxic_train_pruned = data[data['split']=='train' ][data['wiki_topic'].isin(topic_categories[1]+topic_categories[2])]
toxic_test = data[data['split']=='test']
toxic_dev = data[data['split']=='dev']
```
*****************************************************
File description: 

__*topics.pdf*__: shows the 20 topics extracted from *Wiki*-dataset. Each topic is represented by 10 keywords.  


__*wiki_lda_topics.ipynb*__: trains an LDA topic model on the *Wiki*-dataset. Then, uses this model to find the distribution of topics in two other datasets *Waseem*-dataset and *Founta*-dataset. This notebook can be run on Google-colab. 

__*wiki_toxicity_topics.csv*__: each row corresponds to one comment of the *Wiki*-dataset, including comment id, topic number with the highest probability for that comment and the associated probability. 

****************************************************
For more information, please refer to the paper. 

Contact: 

isar.Nejadgholi@nrc-cnrc.gc.ca 

*****************************************************
Terms of Use: 

1. The code can be used freely for non-commercial research and educational purposes.

2. Do not redistribute the code. 

3. National Research Council Canada (NRC) disclaims any responsibility for the use of the codes listed here and does not provide technical support. 

***************************************
