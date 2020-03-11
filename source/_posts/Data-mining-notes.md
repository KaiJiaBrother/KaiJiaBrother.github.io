---
title: Data mining notes & weka notes
tags: Data mining
categories: Notes
abbrlink: c94f917b
date: 2020-02-20 11:04:59
---
# Information Extraction
## Information Extraction(IE) and Information Retrieval(IR)
IE pulls facts and structured information from the content of large text collections (usually corpora).
IR pulls documents from large text collections (usually the Web) in response to specific keywords or queries.
With traditional query engines, getting the facts can be hard and slow.
- IE would return information in a structured way
- IR would return documents containing the relevant information somewhere (if you were lucky)
IE returns knowledge at a much deeper level than IR.
When would you use IE?
- For access to news
- For access to scientific reports
##  Named Entity Recognition
Identification of proper names in texts, and their classification into a set of predefined categories of interest

## MUSE – MUlti-Source Entity Recognition
An IE system developed within GATE


# Language and Computers
## Document classification = sort documents into user-defined classes
classification tasks, such as sentiment analysis
One simple technique for identifying languages is to use `n-grams`(stretch of n tokens(i.e., letters or words)).
Document classification is an example of a computer science activity called machine learning, which is itself part of the subfield of artificial intelligence

Supervised learning: training set and test set have been labeled with desired “correct answers”.
Unsupervised learning: assume there are no pre-specified categories.

First step in classifying or clustering documents:
identify properties most relevant to the decision we want to make, i.e., features
To make a useful system we need to tell the computer two things:
1. Exactly which features are used and exactly how to detect them
- feature engineering
- Hard to automate this step
2. How to weight the evidence provided by the features
- Often works well to use machine learning for this
feature engineering:
- Kitchen sink strategy
- Hand-crafted strategy
The best features may be hard to collect reliably
bag of words assumption
Imagine that we cut up a document and put the words in a bag
Record the odds ratio for ham to spam as 12.5/0.8.
Idea of Naive Bayes: count things that occur in the test set

## authorship attribution
Stylometry
Lexical style markers

## plagiarism

# Data Warehousing
## Introduction
We have lots of data, the point of data mining is to extract the information, knowledge and particularly get the right knowledge at the right time. The idea of data Warehousing is to make data avaliable to do data mining. you need to have a static snap-shot of data to do the evaluation.

## Definition
- a standardized data store
- a process for bringing together disparate data from throughout an organization for decision-support purposes.

use different algorithms to compare results to know which algo is better to use the same data.
store in the database rather in one format.

subject-oriented: discriminating similar languages, has a particular topic
integrated: harvested from different sources into a single standard format(database, social media)
time-variant: twitter, news(data change every time, not predicting in the future)
non-volatile: static snap-shot, use the same dataset(pick the data at a particular time)

copy of transaction data, query and analysis

## Data Mart
smaller, more focused data warehouse - a mini-warehouse
reflects the business rules of a specific business unit within an enterprise.

## Generic Architecture of Data
transaction data: base level of data- raw material for understanding customer behavior
operational sumamary data: summaries are for a specific time period and utilize the transaction data for that time period.
decision support summary data: used to help make decisions about the business.
database schema: defines the structure of data, not the values of the data.
metadata: data
business rules: highest level of abstraction from operational data.
OLAP(ONline Analytical Processing): Data representation for ease of visualization.

is any data-set a data warehouse?
sis: no
library catalogue: no
vle: no
text in a textbook: yes
