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

After preparing this LendingClub dataset for training and testing, we first oversampled the data using **Naive Random Oversampling**. With this we take random "High Risk" samples until it matches up with the rest. This, however, gave us 65 per cent accuracy with a confusion matrix (predicted against actual) array of 
![This is an image](https://myoctocat.com/assets/images/base-octocat.svg)




