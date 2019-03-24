---
layout: post
title: Supervised vs Unsupervised Machine Learning
# subtitle: How to get the elements from a list using Map
tags: [supervsied machine learning, unsupervised machien learning, ML]
---

# Supervised vs Unsupervised Machine Learning

## Supervised Machine Learning

In supervised machine learning we feed the model a dataset that we have the asnwers to. 
In othe words, we have labels that are associated with the training dataset which are used to correct the algorithm. 

The clean dataset will be fed to a model for processing and eventually the model will make some prediction based on the pattern it finds in the attributes of that dataset.

Our dataset consists of rows and columns. Row are called *Observations* and columns are called *attributes*.


## Unsupervised Machine Learning

In unsupervied Machine Learning there is no existing dataset labels. Basically in unsupervised ML, there is no training dataset and the outcomes are unknown. The model goes into the problem blindly. For example in case of detecting images of humans vs cats.

Contrary to supervised learning, in unsupervised learning the model has to be setup right to learn structure in the data. In this case there are no labels that can be used to correct the model instead the model has to be setup just right to learn the patterns or structure.

## Machine Learning Process

1. Collect data
2. Cleanse data
3. Model building. Modeling involves feeding data to mathematical equations.
4. Prediction: Once the model has been tuned and tested, it is ready for use. The idea is that the model should perform well on datasets that has never seen.

### Supervised Learning Tasks

Most common type of applied machine learning is classification
#### Classification

When data is used to predict a category, supervised learning is also called _classification_

#### Linear Regression
When a value is being predicted, like with stock prices, supervised learning is called regression. This is usefull to finding relationships between two continues variables.i.e. Predicting housing prices or stock prices are examples of linear regression.
The idea is figure out a line that best fits the data.

### Unsupervised Learning Tasks
#### Clustering
In this technique, the idea is to group data points.
Given a set of datapoints we can use algorithem to classify each data point into a specific group.

In theory, datapoint within a same group should have similar properties.

#### Associations
In association we look for combination of items that occur together frequently in transactions (mainly used in large dbs or datasets).
The goal is to find associations of items that occur together more often than you would expect in a random sample. The famous example is the beer and diaper association.

## SciKit
Used for building ML models. It is not used for DL models rather for traditioanl models.
After data wrangling and model selection there are 3 things you need to do with every model.
### 1. Fit the model

Training part of data modeling process

### 2. Predict method
Classify incomfing data points
here we make prediction base on the patterns found in the data.

### 3. Evaluate
determine the accuracy of the model.
