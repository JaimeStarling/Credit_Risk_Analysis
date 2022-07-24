# Credit Risk Analysis

## Overview
Good loans greatly outnumber bad loans, but bad loans reduce the opportunity for providing even more good loans. Lowering the risk of unpaid loans is key to providing financial help to an expanded clientele. Using the credit card credit dataset from LendingClub, a peer-to-peer lending services company, we ran different algorithms and compared two machine-learning models.

## Data 
The data itself covers the first calendar year quarter (January, February, March) of 2019, with over 100,000 individual loan requests adding up to nearly $2 billion. Removing requests with missing information, we now had 68,817 loans with completed information. Most were considered "Low Risk" but others were designated "High Risk" if the status was:
- Late (31-120 days)
- Late (16-30 days)
- Default
- In Grace Period

## Oversampling
We know that there are only a few "High Risk" loans among the nearly 69K requests, so the data is considered imbalanced. One way we can "balance" this out is with oversampling. 

After preparing this LendingClub dataset for training and testing, we first oversampled the data using **Naive Random Oversampling**. With this we take random "High Risk" samples until it matches up with the rest. This, however, gave us *65 percent accuracy* with a confusion matrix (predicted against actual) array of: 

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/nro%20confusion%20matrix.png)

To understand the Classification Reports below, we share a quick guide:

pre: precision
rec: recall
spe: specificity
f1: F1 Score
geo: geometric mean
iba: index balanced accuracy
sup: support

The Classification Report, with "High Risk" identified below as "0" in the first line, shows a significantly lower precision rate than the "Low Risk" identified as "1" in the second line. This is also true in the F1 Score, also known in statistics as "the harmonic mean" between precision and recall.

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/nro%20imbalanced%20classification%20report.png)

The *Synthetic Minority Oversampling Technique (SMOTE)* is another oversampling approach to deal with unbalanced datasets like this one. While similar to Naive Randome Oversampling, SMOTE stands out by creating new samples that are similar to the minority set. If a "High Risk" is A and another one is B, SMOTE creates one that's A.5 for the analysis. A and B are real, A.5 is synthesized, but A.5 can be used to bulk up the minority set for balance.

However, SMOTE gave us an *accuracy rate of 62 percent*, lower than the previous oversampling, with a confusion matrix array of:

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/smote%20confustion%20matrix.png)

While there is some improvement with SMOTE in terms of precision rates and F1 Scores, it is not much better.

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/smote%20imbalanced%20classification%20report.png)

## Undersampling

Another way to balance the data set is undersampling. Undersampling takes the opposite approach of oversampling. Instead of increasing the number of the minority class, the size of the majority class is decreased. *Cluster Centroid Undersampling* is akin to SMOTE. The algorithm identifies clusters of the majority class, then generates synthetic data points, called centroids, that are representative of the clusters. The majority class is then undersampled down to the size of the minority class. 

In this algorithm, we got an *accuracy rate of 51 percent*, increasingly worse results than oversampling, with an array of:

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/centroid%20array.png)

Granted, the precision rates and F1 Scores are improved.
![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/centroid%20classification.png)

## Combination Sampling

*SMOTEENN* combines the SMOTE and *Edited Nearest Neighbors (ENN)* algorithms, combining oversampling and undersampling in a two-step process that begins with SMOTE and then cleaning the data again with undersampling. The resulting accuracy rate was 64 percent, not much different than Naive Random Sampling, but with a more interesting array and improved F1 Scores:

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/centroid%20array.png)

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/smoteen%20classification.png)

## Ensemble Classifiers

We then tried the *Balanced Random Forest Classifier* on the dataset. This is an extension of bagging, fitting multiple models on different subsets of a training dataset, then combining the predictions from all models. Not always recommended, this algorithm did provide decent results with an *accuracy rate of 79 percent*! The array is a real change as well:

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/brf%20array.png)

The F1 Scores are greatly improved:

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/brf%20classification.png)

Finally we tried the *Easy Ensemble AdaBoost Classifier*, which [Kaggle](https://www.kaggle.com/code/prashant111/adaboost-classifier-tutorial/notebook) describes as "an iterative ensemble method. AdaBoost classifier builds a strong classifier by combining multiple poorly performing classifiers so that you will get [a] high accuracy strong classifier." And how! *The accuracy rate was 99 percent*. Unfortunately, such a high accuracty rate is a warning that something is not right. Here are the arrays and classifications, but they should not be considered:

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/ada%20array.png)

![This is an image](https://github.com/JaimeStarling/Credit_Risk_Analysis/blob/main/Images/ada%20classification.png)


