
This work is done by Rochester Human-Computer Interaction (ROC HCI) lab, University of Rochester, USA with the collaboration of Language Technologies Institute, SCS, CMU, USA.

ROC-HCI Website: (https://roc-hci.com/) 

# UR-FUNNY
 
1. This repository includes the UR-FUNNY dataset: first dataset for *multimodal humor detection* .
2. It has the tutorial about how to read the dataset.
3. It has the code of Contextual Memory Fusion Netowrk for humor detection.

Please read the folllwoing paper for the details of the dataset and models. You can cite the paper:

Hasan, Md Kamrul, Wasifur Rahman, Amir Zadeh, Jianyuan Zhong, Md Iftekhar Tanveer, Louis-Philippe Morency and Mohammed (Ehsan) Hoque. "UR-FUNNY: A Multimodal Language Dataset for Understanding Humor", EMNLP, 2019. link: (https://www.aclweb.org/anthology/D19-1211/)


# Dataset

You can find the version of the dataset that we used in the EMNLP paper in the following link: (https://github.com/ROC-HCI/UR-FUNNY/blob/master/UR-FUNNY-V1.md)

## UR-FUNNY-V2
We have created second version of the dataset which removes nosiy data instances and the humor insatnces has no overlap. This new version also has more context sentences. You will also find the raw videos in here. The format of this version is simialr to previous one. Please read the followings for details about the extracted features. 

raw videos: (https://www.dropbox.com/s/lg7kjx0kul3ansq/urfunny2_videos.zip?dl=1)  
extracted features: (https://www.dropbox.com/sh/9h0pcqmqoplx9p2/AAC8yYikSBVYCSFjm3afFHQva?dl=1)


In the extracted features folder, it has five pkl files:

1. data_folds 
2. langauge_sdk
2. openface_features_sdk
3. covarep_features_sdk
4. humor_label_sdk
5. word_embedding_list



## Data folds:

data_folds.pkl has the ductionary that contains train, dev and test list of humor/not humor video segments **id**. 


## Langauge Features:

word_embedding_list.pkl has the list of word embeddings of all unique words that are present in the UR-FUNNY dataset. We use the **word indexes** from this list as language feature. Later we can use these **word indexes** to retrive the glove embedding of those words. We followed this approach to reduce the space. Because same word appears multiple times.


language_sdk.pkl contains a dictionary. All the keys are the **id** of the humor / not humor video segments. This **id** wll also match with raw video name.

The structure of the dictionary:

```
word_embedding_indexes_sdk{
	id1: {
		punchline_embedding_indexes : [ idx1,idx2,.... ]
		context_embedding_indexes : [[ idx2,idx30,.... ],[idx5,idx6......],..]	
		punchline_sentence : [....]
		context_sentences : [[sen1], [sen2],...]
		punchline_intervals : [ intervals of words in punchline ]
		context_intervals : [[ intervals of words in sen1 ], [ intervals of words in sen2 ],.......]
		}
	id2: {
		punchline_embedding_indexes : [ idx10,idx12,.... ]
		context_embedding_indexes : [[ idx21,idx4,.... ],[idx91,idx100......],..]	
		punchline_sentence : [....]
		context_sentences : [[sen1], [sen2],...]
		punchline_intervals : [ intervals of words in punchline ]
		context_intervals : [[ intervals of words in sen1 ], [ intervals of words in sen2 ],.......]				 
		}
	.....
	.....
}
```

Each video segments has two kind of features: 

1. punchline_features: It contanis the list of **word indexes** (descibed above) of punchline sentence. The dimension of word index is 1. We will use this word index to retrive the word embedding (glove.840B.300d) from word_embedding_list (described above). So if the punchline has n words then the dimension will be n * 1.

2. context_features: It contanis the list of **word indexes** for the sentences in context. It is three dimensional list. 1st dimension is number of sentences in context. Second dimension is number of word for each sentence. 3rd dimension is the dimension of word index which is 1.



## Acoustic Features:

covarep_features_sdk.pkl contains a dictionary. All the kyes are the **id** of the humor/not humor video segments.

The structure of the covarep_features_sdk:

```
covarep_features_sdk{
	id1: {
		punchline_features : [ [ .... ],[ .... ], ...]
		context_features : [ [[ .... ],[......],..], [[ .... ],[......],..], ... ]							 	....
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

openface_features_sdk.pkl contains a dictionary. All the kyes are the **id** of the humor/not humor video segments. We have used OpenFace2 (https://github.com/TadasBaltrusaitis/OpenFace) to extract the fetaures.

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

1. punchline_features: It contanis the average openface features for each word in the punchline sentence. We aligned our features on word level. The dimension of openface fetaures is 371. So if the punchline has n words then the dimension will be n * 371.
2. context_features: It contanis the average openface features for each word in the context sentences. It is three dimensional list. 1st dimension is number of sentences in context. Second dimension is number of word for each sentence. 3rd dimension is the dimension of openface fetaures (371).

## Humor Labels:

humor_label_sdk.pkl contains a dictionary. All the kyes are the **id** of the humor/not humor video segments.

For each id the value is either 1 or 0.

- 1 = means this video segment has humorours puncline
- 0 = means this video segment does not have humorous punchline 


# Data Loading Tuitorial

**Prerequistie**: python 3.5, pickle, pytorch

humor_dataloader.ipynub is the tutorial for loading UR-FUNNY dataset. It has details instruction about how to design Dataset class and Dataloader for UR-FUNNY dataset in pytorch. It also show how to read the punchline features, context features and humor label using the dataloader.   


# Contextual Memory Fusion Netowrk for Humor Detection

The github link of the code for Contextual Memory Fusion Netowrk of Humor Detection : ***coming Soon***
