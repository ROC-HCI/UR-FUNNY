# UR-FUNNY

1. This repository includes the UR-FUNNY datset: first dataset for *multimodal humor detection* .
2. It has the tutorial about how to read the dataset.
3. It has the code of Contextual Memory Fusion Netowrk for humor detection.

Please read the folllwoing paper for the details of the dataset and models. 

Hasan, Md Kamrul, Wasifur Rahman, Amir Zadeh, Jianyuan Zhong, Md Iftekhar Tanveer, Louis-Philippe Morency and Mohammed (Ehsan) Hoque. "UR-FUNNY: A Multimodal Language Dataset for Understanding Humor", EMNLP, 2019. (accepetd) 


# Dataset

The link of the  preprocessed features: [humor dataset](https://www.dropbox.com/s/izk6khkrdwcncia/ted_humor_sdk_v1.zip?dl=1)


It has five pkl files:

1. data_folds 
2. word_embedding_indexes_sdk
2. openface_features_sdk
3. covarep_features_sdk
4. humor_label_sdk
5. word_embedding_list



## Data folds:

data_folds.pkl has the ductionary that contains train, dev and test list of humor/not humor video segments **id**. 


## Langauge Features:

word_embedding_list.pkl has the list of word embeddings of all unique words that are present in the UR-FUNNY dataset. We use the **word indexes** from this list as language feature. Later we can use these **word indexes** to retrive the glove embedding of those words. We followed this approach to reduce the space. Because same word appears multiple times.


word_embedding_indexes_sdk.pkl contains a dictionary. All the keys are the **id** of the humor / not humor video segments. 

The structure of the dictionary:

```
word_embedding_indexes_sdk{
	id1: {
		punchline_embedding_indexes : [ idx1,idx2,.... ]
		context_embedding_indexes : [[ idx2,idx30,.... ],[idx5,idx6......],..]	
									 
		}
	id2: {
		punchline_embedding_indexes : [ idx10,idx12,.... ]
		context_embedding_indexes : [[ idx21,idx4,.... ],[idx91,idx100......],..]	
									 
		}
	.....
	.....
}
```

Each video segments has two kind of features: 

1. punchline_features: It contanis the list of **word indexes** (descibed above) of punchline sentence. The dimension of word index is 1. We will use this word index to retrive the word embedding from word_embedding_list (described above). So if the punchline has n words then the dimension will be n * 1.

2. context_features: It contanis the list of **word indexes** for the sentences in context. It is three dimensional list. 1st dimension is number of sentences in context. Second dimension is number of word for each sentence. 3rd dimension is the dimension of word index which is 1.



## Acoustic Features:

covarep_features_sdk.pkl contains a dictionary. All the kyes are the **id** of the humor/not humor video segments.

The structure of the covarep_features_sdk:

```
covarep_features_sdk{
	id1: {
		punchline_features : [ [ .... ],[ .... ], ...]
		context_features : [ [[ .... ],[......],..], [[ .... ],[......],..], ... ]							 
		}

	id2:{
		punchline_features : [ [ .... ],[ .... ], ...]
		context_features : [ [[ .... ],[......],..], [[ .... ],[......],..], ... ]
		....
	}
	....
	....
}
```

Each humor/not humor video segment has two kind of features:

1. punchline_features: It contanis the average covarep features for each word in the punchline sentence. We aligned our features on word level. The dimension of covarep fetaures is 81. So if the punchline has n words then the dimension will be n * 81.
2. context_features: It contanis the average covarep features for each word in the context sentences. It is three dimensional list. 1st dimension is number of sentences in context. Second dimension is number of word for each sentence. 3rd dimension is the dimension of covarep fetaures (81).



## Visual Features:

openface_features_sdk.pkl contains a dictionary. All the kyes are the **id** of the humor/not humor video segments.

The structure of the openface_features_sdk:

```
openface_features_sdk{
	id1: {
		punchline_features : [ [ .... ],[ .... ], ...]
		context_features : [ [[ .... ],[......],..], [[ .... ],[......],..], ... ]							 
		}

	id2:{
		punchline_features : [ [ .... ],[ .... ], ...]
		context_features : [ [[ .... ],[......],..], [[ .... ],[......],..], ... ]
		....
	}
	....
	....
}
```

Each humor/not humor video segment has two kind of features:

1. punchline_features: It contanis the average openface features for each word in the punchline sentence. We aligned our features on word level. The dimension of openface fetaures is 75. So if the punchline has n words then the dimension will be n * 75.
2. context_features: It contanis the average openface features for each word in the context sentences. It is three dimensional list. 1st dimension is number of sentences in context. Second dimension is number of word for each sentence. 3rd dimension is the dimension of openface fetaures (75).

## Humor Labels:

humor_label_sdk.pkl contains a dictionary. All the kyes are the **id** of the humor/not humor video segments.

For each id the value is either 1 or 0.

- 1 = means this video segment has humorours puncline
- 0 = means this video segment does not have humorous punchline 


# Data Loading Tuitorial

**Prerequistie**: python 3.5, pickle, pytorch

humor_dataloader.ipynub is the tutorial for loading UR-FUNNY dataset. It has details instruction about how to design Dataset class and Dataloader for UR-FUNNY dataset in pytorch. It also show how to read the ounchline features, context features and humor label using the dataloader.   


# Contextual Memory Fusion Netowrk for Humor Detection

The github link of the code for Contextual Memory Fusion Netowrk of Humor Detection : ***coming Soon***