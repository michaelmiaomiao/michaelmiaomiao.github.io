---
layout:     post
title:      Machine Learning Application on Heart Disease Prediction  
subtitle:   Preventing heart disease is important. Good data-driven systems for predicting heart disease can improve the entire research and prevention process, making sure that more people can live healthy lives.
date:       2019-08-30
author:     Jiashu Miao
header-img: 
catalog: true
tags:

    - Python
    - Machine Learning
    - Classification
    - Project 
    
---


### About （from: [DrivenData](https://www.drivendata.org/competitions/54/machine-learning-with-a-heart/page/108/)）

In the United States, the Centers for Disease Control and Prevention is a good resource for information about heart disease. According to their website:

About 610,000 people die of heart disease in the United States every year–that’s 1 in every 4 deaths.
Heart disease is the leading cause of death for both men and women. More than half of the deaths due to heart disease in 2009 were in men.
Coronary heart disease (CHD) is the most common type of heart disease, killing over 370,000 people annually.
Every year about 735,000 Americans have a heart attack. Of these, 525,000 are a first heart attack and 210,000 happen in people who have already had a heart attack.
Heart disease is the leading cause of death for people of most ethnicities in the United States, including African Americans, Hispanics, and whites. For American Indians or Alaska Natives and Asians or Pacific Islanders, heart disease is second only to cancer.
For more information, you can look at the website of the Centers for Disease Control and Prevention:
[prventing heart disease](https://www.cdc.gov/heartdisease/prevention.htm)


### Progress

- Explore data
- Investigate data 
- Clean and manipulate data
- Transform and encode data

### Problem need to solve:

I find the distribution of the testing and training data for 2 variables are different, which will undoubtly affect the accuracy of the predictive result. 

- as shown: 

![](https://michaelmiaomiao.github.io/webfile/Untitled.png)
![](https://michaelmiaomiao.github.io/webfile/DD2.png)

In order to fix the problem, I am still considering resample or shuffle the data, while this manipulation will create noises.

The trade of noise and variance is cruicial because it will make differences on accuracies when comming to competition level predictive analysis

### Sample code (will be available after the competition)

![](/img/DDsamplecode.png)
