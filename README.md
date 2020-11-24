
This work is done by Rochester Human-Computer Interaction (ROC HCI) lab, University of Rochester, USA with the collaboration of Language Technologies Institute, SCS, CMU, USA.

ROC-HCI Website: (https://roc-hci.com/) 

# UR-FUNNY
 
1. This repository includes the UR-FUNNY dataset: first dataset for *multimodal humor detection* .
2. It has the tutorial about how to read the dataset.
3. It has the code of Contextual Memory Fusion Netowrk for humor detection.

Please read the folllwoing paper for the details of the dataset and models.

Hasan, Md Kamrul, Wasifur Rahman, Amir Zadeh, Jianyuan Zhong, Md Iftekhar Tanveer, Louis-Philippe Morency and Mohammed (Ehsan) Hoque. "UR-FUNNY: A Multimodal Language Dataset for Understanding Humor", EMNLP, 2019. link: (https://www.aclweb.org/anthology/D19-1211/)


# Dataset

You can find the first version of the dataset that we used in the EMNLP paper in the following link: (https://github.com/ROC-HCI/UR-FUNNY/blob/master/UR-FUNNY-V1.md)

## UR-FUNNY-V2
We have created second version of the dataset by removing the nosiy and overlapping data instances. This new version has more context sentences. We have added the link of the raw video here. The format of this version is simialr to previous one. Please read the followings for the details about the extracted features. 

**Raw Videos**: (https://www.dropbox.com/s/lg7kjx0kul3ansq/urfunny2_videos.zip?dl=1)  
**Extracted Features**: (https://www.dropbox.com/sh/9h0pcqmqoplx9p2/AAC8yYikSBVYCSFjm3afFHQva?dl=1)
**Transcripts**: You will find the transcript in language_sdk.pkl described below.

There are six pickle files in the extracted features folder:

1. data_folds 
2. langauge_sdk
3. openface_features_sdk
4. covarep_features_sdk
5. humor_label_sdk
6. word_embedding_list



## Data folds:

data_folds.pkl has the dictionary that contains train, dev and test list of humor/not humor video segments **id**. These folds are speaker independent and homogenous. Please use these folds for valid comparison.


## Langauge Features:

word_embedding_list.pkl has the list of word embeddings of all unique words that are present in the UR-FUNNY dataset. We use the **word indexes** from this list as language feature. These **word indexes** are used to retrive the glove embeddings of the corresposnding words. We followed this approach to reduce the space. Because same word appears multiple times.


language_sdk.pkl contains a dictionary. The keys of the dictionary are the unique **id** of each humor / not humor video utterance. The corresponding raw video uttereances are also named by these unique **id**'s.

The structure of the dictionary:

```
langauge_sdk{
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

Each video segments has four kind of features: 

1. punchline_features: It contanis the list of **word indexes** (described above) of punchline sentence. We will use this word index to retrive the word embedding (glove.840B.300d) from word_embedding_list (described above). So if the punchline has n words then the dimension will be n.

2. context_features: It contanis the list of **word indexes** for the sentences in context. It is two dimensional list. First dimension is the number of sentences in context. Second dimension is the number of word for each sentence.

3. punchline_sentence: It contains the punchline sentence

4. context_sentences: It contanis the sentences used in context


## Acoustic Features:

covarep_features_sdk.pkl contains a dictionary. The keys of the dictionary are the unique **id** of each humor / not humor video utterance. We used COVAREP (https://covarep.github.io/covarep/) to extract acoustic features. See the extracted_features.txt for the names of the features.

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
2. context_features: It contanis the average covarep features for each word in the context sentences. It is a three dimensional list. First dimension is the number of sentences in context. Second dimension is the number of word for each sentence. Third dimension is the dimension of covarep fetaures (81).



## Visual Features:

openface_features_sdk.pkl contains a dictionary. The keys of the dictionary are the unique **id** of each humor / not humor video utterance. We have used OpenFace2 (https://github.com/TadasBaltrusaitis/OpenFace) to extract the fetaures. See the extracted_features.txt for the names of the features.

The structure of the openface_features_sdk:

```
openface_features_sdk{
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

1. punchline_features: It contanis the average openface features for each word in the punchline sentence. We aligned our features on word level. The dimension of openface fetaures is 371. So if the punchline has n words then the dimension will be n * 371.
2. context_features: It contanis the average openface features for each word in the context sentences. It is a three dimensional list. First dimension is the number of sentences in context. Second dimension is the number of word for each sentence. Third dimension is the dimension of openface fetaures (371).

## Humor Labels:

humor_label_sdk.pkl contains a dictionary. All the kyes are the **id** of the humor/not humor video segments.

For each id the value is either 1 or 0.

- 1 = means this video segment has humorours puncline
- 0 = means this video segment does not have humorous punchline 


# Data Loading Tuitorial

**Prerequistie**: python 3.5, pickle, pytorch

humor_dataloader.ipynub is the tutorial for loading UR-FUNNY dataset. It has details instruction about how to design Dataset class and Dataloader for UR-FUNNY dataset in pytorch. It shows how to read the punchline features, context features and humor label using the dataloader.   

