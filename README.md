# Introduction
<p align = "justify">
In this repository I am showing the model that I used in the <a href="https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge">Toxic Comment Classification Challenge </a> hosted by kaggle, in this competition, we have to build a multi-headed model that’s capable of detecting different types of of toxicity like threats, obscenity, insults, and identity-based hate. To train the models a dataset of comments from Wikipedia’s talk page edits was available, this data set contains text that may be considered profane, vulgar, or offensive.
</p>

# Data set description
<p align = "justify">
The data correspond to comments from Wikipedia’s talk page edits, it can be access from the <a href = "https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data"> competition page </a>. As usual in kaggle competitions, the data is split into training and test sets.
</p>
The columns in the training set are as follows:

|Column      | Description                                                       |
|------------|-------------------------------------------------------------------|
|id          | Text id of the row                                                |
|comment_text| This contains the text that we need to classify                   |
|classes     | There are six columns representing the classes, each one is binary|

In a similar way the test set contains the same columns, except the last one.

# Model
To handle this problem I used an ensemble model composed of ensemble models, basically I used four
![Model Description](model.png)

# Reproducibility
<p align = "justify">
To run the model, you need to download this reposiotory, it is necesary to have all the necesary dependencies listed in the table below, the versions have not necessary to be the same, but be aware that some package could not work well with lower versions, also this model was trained in a Ubuntu OS, therefore, you can install all the dependencies from the terminal, the data sets can be access from the <a href = "https://www.kaggle.com/c/jigsaw-toxic-comment-classification-challenge/data"> competition page </a>, once they are downloaded you need to put them in a folder named <b>data</b> at the same level that the <b>model</b> folder and run the notebook.
</p>

|       Package     |      Version      |
|-------------------|-------------------|
| numpy             |       1.14.0      |
| pandas            |       0.22.0      |
| scikit-learn      |       0.19.1      |
| catboost          |       0.6.2       |
| anaconda          |       5.1.0       |
|	jupyter 	        |       5.4.0       |
| python            |       3.6.4       |

# Results
<p align="justify">
At the end of the competition the model obtained a score of 0.9566 in the private leaderboard. I think that it could achieve greater results, if it was trained more times and if other strategies had been applied.
</p>
