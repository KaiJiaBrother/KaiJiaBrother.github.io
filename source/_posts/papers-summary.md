---
title: papers summary
tags: papers
categories: papers
abbrlink: 7cd80329
date: 2020-03-20 23:45:21
---
{% cq %}A summary of the papers that I read for the project.{% endcq %}
<!-- more -->
{% note danger no-icon %}
Please provide a brief summary including
1. What did they do and why?
2. What did they find?
3. Are there any issues/challenges with the research?
4. How is their work relevant to your project?
{% endnote %}

{% note info no-icon %}
N. Valakunde and S. Ravikumar, "Prediction of Addiction to Social Media," 2019 IEEE International Conference on Electrical, Computer and Communication Technologies (ICECCT), Coimbatore, India, 2019, pp. 1-6.

1. The problem of social media addiction has only been observed and studied in the previous research papers, but no solution has been presented to date. This study aims to solve the problem of addiction by implementing machine learning using Linear Regression through Least Square Method and recommending certain positive exercises and practices which can help an individual to refrain from high usage of social media.

2. The data collected is analyzed with the help of graphs plotted by using the users' data. The inputs are taken from the user from the respective questions asked to him/her, and a point is plotted for the user's values in the respective graphs. By plotting the points on these graphs and comparing them, the machine is able to determine the problem faced by an individual and help him/her by giving out suggestions in the form of helpline numbers, motivational videos and/or inspiring speeches from successful people. This is a small and effective method to help people get rid of addiction to social media and lead a better life.

3. The research uses a very simple and basic algorithm(Linear Regression using Least Square Method). More complex and advanced machine learning algorithms can be used to achieve higher levels of accuracy in predictions. Besides, the research only contains the user data collected of 287 users, more data should be collected to make result become much more intelligent and accurate.

4. The research uses Linear Regression algorithm to indicate whether the user is addicted to social media or not and gives some recommendation to them like cutting down on their social media usage. This work can be used to predict the user behaviors to indicate how much the user would get addicted to the social media.
{% endnote %}

{% note warning no-icon %}
M. Meghawat, S. Yadav, D. Mahata, Y. Yin, R. R. Shah and R. Zimmermann, "A Multimodal Approach to Predict Social Media Popularity," 2018 IEEE Conference on Multimedia Information Processing and Retrieval (MIPR), Miami, FL, 2018, pp. 190-195.

1. First, they use a random forest approach on available social and contextual information. Next, they apply a CNN model on available social and contextual information. Moreover, they apply transfer learning on image content information using the pre-trained InceptionResnet V2 model. Finally, in their multimodal approach, they combine all features derived from earlier steps and apply a convolutional model. The first reason is that most of previous researches just focused on information provided in the SMP-T1 dataset which includes average counts for views, comments, tags, groups, members, and lengths of title and description. No such multimodal dataset exists for the prediction of social media photos. So they propose a new dataset, called multimodal-SMP-dataset, by augmenting the existing SMP-T1 dataset with additional contextual information such as titles, descriptions, and tags of social media photos in addition to crawling image content (actual photos). The second reason is that one modality might not be enough to solve a complex problem like popularity prediction, so their proposed system exploits multimodal information.

2. Experimental results confirm that despite they use half of the training set, their multimodal approach gives comparable performance to that of state-of-the-art. Moreover, they have provided a multimodal dataset for social media popularity prediction to research community.

3. In their research, they explored different models for social media popularity prediction and got different results (Spearman RHO, Mean Absolute Error (MAE), and Mean Squared Error (MSE)) for each model. The issue is that they didn't mention how many times they did those experiments for each model. I do not know whether they used an average result of several experiments or just an optimal result of single experiment.

4. This research uses a multimodal approach to predict the social media popularity, which could help me consider to use a multimodal approach (including image content) to do my project instead of focusing on a single model. Besides, it reminds me that I could also expand the dataset if necessary.
{% endnote %}

{% note success no-icon %}

{% endnote %}
