---
layout:     post
title:      Data Science Knowledge Complete Summary (continuosly updated)
subtitle:   This is a data-science concept post edit and organized by me to summarize and sort out cs, stats, machine learning and other related topics all in one from past learning.
date:       2019-10-24
author:     Jiashu Miao
header-img: 
catalog: true
tags:

    - R
    - Data Science 
    - Cheat Sheet
    - Statistics
    
---


## Data Science 

Multi-disciplinary field that brings together concepts from computer science, statistics/machine learning, and data analysis to understand and extract insights from the ever-increasing amounts of data.

1. Hypothesis-Driven: Given a problem, what kind of data do we need to help solve it?

2. Data-Driven: Given some data, what interesting problems can be solved with it

3. what can we learn from data and what actions to take?

## Types of data 

1. **Structured**: Data that has predefined structures. e.g. tables, spreadsheets, or relational databases.

2. **Unstructured Data:**: Data with no predefined struc- ture, comes in any size or form, **CANNOT be** easily stored in tables. e.g. blobs of text, images, audio

3. **Quantitative Data**: Numerical. e.g. height, weight 

4. **Categorical Data**: Data that can be labeled or divided into groups. e.g. race, sex, hair color.

5. **Big Data**: Massive datasets, or data that contains; greater variety arriving in increasing volumes and with ever-higher velocity (3 Vs). Cannot fit in the memory of a single machine.

### Data Source / Format


#### Most Common Data Formats

CSV, XML, SQL, JSON, Protocol Bu↵ers

#### Data Sources 

Companies/Proprietary Data, APIs, Gov- ernment, Academic, Web Scraping/Crawling




### Data Science Problem Types:

#### **Classification**: 
Assigning something to a discrete set of possibilities. e.g. spam or non-spam, Democrat or Repub- lican, blood type (A, B, AB, O)

#### **Regression**: 
Predicting a numerical value. e.g. some- one’s income, next year GDP, stock price


## Probablity

Probability theory provides a framework for reasoning about likelihood of events.


#### Experiment: 
procedure that yields one of a possible set of outcomes e.g. repeatedly tossing a die or coin.

#### Sample Space S:
set of possible outcomes of an experi- ment e.g. if tossing a die, S = (1,2,3,4,5,6)

#### Event E: 
set of outcomes of an experiment e.g. event thatarollis5,ortheeventthatsumof2rollsis7

#### Probability of an Outcome
s or P(s): number that *satisfies 2 properties*.


$$ 0\leq P(s) \leq 1 $$

$$ \sum P(s) = 1 $$


#### Probability of Event E:
sum of the probabilities of the outcomes of the experiment:
$$ p(E) = \sum Ps⇢E p(s)$$


#### Random Variable V:
 numerical function on the out- comes of a probability space


#### Expected Value V:
$$ E(V) = \sum(s\space belongs\space to\space s) P(s) * V(s)$$



### Indepedence Conditional Compound


![](https://michaelmiaomiao.github.io/webfile/independence.png)


### Probability Distributions

#### Probability Density Function (PDF): 
Gives the prob- ability that a rv takes on the value x: pX(x) = P(X = x)

#### Cumulative Density Function (CDF) 
Gives the prob- ability that a random variable is less than or equal to x: FX(x)=P(Xx)


**Note**: The PDF and the CDF of a given random variable contain exactly the same information.




## Descriptive Stats:

### Centrality:
#### Arithematic Mean:
best when character symmetric distribution without outliers: 1/n sigma X
#### Geometric Mean: 
Always smaller than arithematic means: useful to capture averaging ratios mean = Nth root of a1 a2 ...a3 

$$ ^n\sqrt{a_{1}*a_{2}* ... * a_{n}}$$
#### median
 
#### mode: 
most frequent value


#### variabiliy:
	
- **standard deviation**: Measure the *square differenc*e between the elements and mean 看每个直的平方和平均值差多少 **REMEMBER TO /(N-1) GIVEN LARGE N FOR DEGREE OF FREEDOM**
- Variance V = SIGMA SQAURE 2

#### variance interpret: 
Variance is an inherent part of the universe. It is impossible to obtain the same results after repeated observations of the same event due to random noise/error. Variance can be explained away by attributing to sampling or measurement errors. Other times, the variance is due to the random fluctuations of the universe.

#### Correlation Analysis: 
Correlation coefficients r(X,Y) is a statistic that measures the degree that Y is a function of X and vice versa. Correlation values range from -1 to 1, where 1 means fully correlated, -1 means negatively-correlated, and 0 means no correlation.

#### Person Coeffcicent: 
- Measures the degree of the relationship between linear related variables: R


#### Spearman Rank Coefficient: 
- Computed on ranks and depicts **monotonic**  ????? relationship

[Check out more about Spearman's Rank Correlation Coefficient](https://geographyfieldwork.com/SpearmansRank.htm)

- A correlation can easily be drawn as a scatter graph, but the most precise way to compare several pairs of data is to use a statistical test - this establishes whether the correlation is really significant or if it could have been the result of chance alone.
- Spearman’s Rank correlation coefficient is a technique which can be used to summarise the strength and direction (negative or positive) of a relationship between two variables.

**Note: Correlation does not imply causation**

![](https://michaelmiaomiao.github.io/webfile/descriptive.png)



------------------------------------------------------------

> edited by Micahel Miao Oct 24th, 2020.


