# UR-FUNNY

1. This repository includes the UR-FUNNY datset: first dataset for *multimodal humor detection* .
2. It also includes the tuitorial about how to read the dataset.
3. It also includes the code of Contextual Memory Fusion Netowrk for humor detection.

Please read the folllwoing paper for the details of the dataset and models. 

Hasan, M. K., Rahman, W., Zadeh, A., Zhong, J., Tanveer, M. I., & Morency, L. P . UR-FUNNY: A Multimodal Language Dataset for Understanding Humor. (Acepted in EMNLP 2019)


#Dataset

The link of the dataset: 

It has five pkl files:

1. data_folds 
2. word_embedding_indexes_sdk
2. openface_features_sdk
3. covarep_features_sdk
4. humor_label_sdk
5. word_embedding_list


######Data folds:

data_folds.pkl has the ductionary that contains train, dev and test list of humor utterance id. 

######Langauge Features:

word_embedding_list.pkl has the list of word embeddings of all unique words presents in the humor dataset. We will use the **word indexes** from thus list as language feature to reduce the feature space.


word_embedding_indexes_sdk.pkl contains a dictionary. All the kyes are the **id** of the humor utterance.

Each utterance has two kind of features: 
	1. punchline_embedding_indexes : Contains the list of **word indexes**(descibed above)  of punchline sentence
	2. context_embedding_indexes: Contains the matrix of all word indexes in context sentences. This matrix is a list of word indexes list. Because conetxt has multiple sentences.   

structure of the dictionary:

```
word_embedding_indexes_sdk{
	hid: {
		punchline_embedding_indexes : [ id1,id2,.... ]
		context_embedding_indexes : [[ id1,id2,.... ],
									  [id5,id6......],	
									  ...
									]
		}
}
```