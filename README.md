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
|classes     | There are six: toxic, severe toxic, obscene, threat, insult and identity hate|

<p align = "justify">
Each class was represented in a column using binary values. In a similar way the test set contains the same columns, except the classes.
</p>

# Model
<p align="justify">
I extract 5000 TF-IDF features from the text data, then I began experimented with a single model, which did not well enoght, then I elaborate another idea, since there was six binary clasess corresponding to each category, I decided to use a single classifier which will learn to recognized each one of them, then combine the results into a single model, but it turn out to be even worst than the single model, then I decided to created a ensamble model to each individual classes, but I see that the more mdels I added the more complex was the ensemble to train, so I decided to add models which where relativaly simple, and that do not have many hyperparameters to tune (since the data set is relativaly large, it could take many hours to train), that way I ended up with four main models:
</p>

- __AdaBoost:__ AdaBoost was prove to have less accuracy, but it achieve aceptable results, also it had no many hyperparameters to tune. Also compared with other tree models it was much faster.
- __BernoulliNB (alpha: 1.0 | alpha: 0.5):__ Surprising, this simple model achieved aceptable results, therefore I decided to add two of them, one using alpha: 1.0 and the other with alpha: 0.5.
- __Ridge Classifier:__ This model was really fast, and it was very accurate too, even more than the other models above.
<p align = "justify">
The next thing that I tried was use the predictions of each single model to construct features to train other model which will be the final one, and after trying with many ones, I chose CatBoost. The main reason to chose CatBoost was that I need thta my final model could be trained using hyperparameters, but at the same time I also do not wanted to have to tune many of them, another factor was that I notice that using a single model to classify each class became a binary problem, and when looked the data I notices that the classes were imbalanced, and CatBoost had a special hyperparameter to deal with that problem, in fact catBoost acted like a pipe wrench, helping me to better tune the predictions of the other models, also the more epoch I gave to catBosst the better were the results, also catBoost do not was affected too much by the lower performance of the other models models.
</p>

All the above could be summarize in the __Figure 1__:

![Models](models.png)

__Figure 1:__ _Models for class k_

<p align = "justify">
Also, the <b>Figure 1</b> a 5000 TF-IDF features were used to feed all the models. Putting alltogheter we have the final model which is described in the <b> Figure 2</b>:
</p>

![Model Description](model.png)
__Figure 2:__ _Final model_


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
