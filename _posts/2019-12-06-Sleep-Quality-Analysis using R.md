---
layout:     post
title:      Sleep Quality Analysis using R
subtitle:   Follow Up previous Python project by re-writting in R.
date:       2019-11-21
author:     Jiashu Miao
header-img: 
catalog: true
tags:

    - R
    - Jupyter
    - Data Exploration
    - Sleep Quality
    
---

## Background Information

### 1.1 Data source
- National Sleep Foundation www.sleepfoundation.org
- 2015 Sleep in America Poll, which we assume their answers reflect true situation

### 1.2 Data Collection & General Information
The National Sleep Foundation counducted an online survey study on sleep of Americans in December 2014 and obtained answers from 1,029 non-institutionalized adults aged 18 years or older who reside in the United States. The survey asked participants about their sleep quality, attitude toward sleep, time spent in bed, estimate of actual sleep obtained, how much do they think certain factors affect their sleep quality, etc.

Participants were selected via representative random sampling on Growth from Knowledge (GfK)’s KnowledgePanel. The KnowledgePanel initially used the Delivery Sequence File (DSF) of the United States Postal Service as the sampling frame to recruit panalists. The DSF covers almost 100% of the U.S. population.

### 1.3 Objective

College students, including myself, have experienced unsatisfactory sleep quality. Especially during exam periods, our peers often express similar concerns as ourselves, that is, we do not have “good” sleep. 

One thing that we have noticed is that with the increasing usage of mobile phones, we spent quite a considerable amount of time messing with our phone in bed before actually falling asleep and after waking up.  

Thus, I wonder whether sleeping efficiency has a relationship with sleep quality, as well as what are potential factors that associate with sleep quality and worh exploration.

### 1.4 Variables and Descriptions

1. `Q10_a`: sleep quality, 5-point Likert Scale (1: very poor, 2: poor, 3: fair, 4: good, 5: very good)
2. `DOV_WEEKTIME`: average minutes spent in bed per day on weekdays
3. `DOV_WEEKEND`: average minutes spent in bed per day on weekends
4. `DOV_TOTALWEEK`: estimate of actual sleep obtained per day on weekdays (in minutes)
5. `DOV_TOTALWEEK`: estimate of actual sleep obtained per day on weekendss (in minutes)
6. `Q2_ampmA`: whether time went to bed on weekdays is a.m. or p.m.
7. `Q3_ampmA`: whether time went to bed on weekends is a.m. or p.m.
8. `Q14a`: how often do health problems make it difficult to get a good night’s sleep, 5-point Likert Scale (1: never, 2: rarely, 3: sometimes, 4: often, 5: always)
9. `Q15_a`: how often does outside noise (ex: street noise, sirens) make it more difficult to get a good night's sleep, 5-point Likert Scale (1: never, 2: rarely, 3: sometimes, 4: often, 5: always)
10. `Q15_b`: how often does inside noise (ex: television, other people, snoring) make it more difficult to get a good night's sleep, 5-point Likert Scale (1: never, 2: rarely, 3: sometimes, 4: often, 5: always)
11. `Q15_c`: how often does light (from either inside or outside) make it more difficult to get a good night's sleep, 5-point Likert Scale (1: never, 2: rarely, 3: sometimes, 4: often, 5: always)
12. `Q15_d`: how often does temperature (too hot or too cold) make it more difficult to get a good night's sleep, 5-point Likert Scale (1: never, 2: rarely, 3: sometimes, 4: often, 5: always)
13. `Q15_e`: how often does temperature (uncomfortable mattress) make it more difficult to get a good night's sleep, 5-point Likert Scale (1: never, 2: rarely, 3: sometimes, 4: often, 5: always)
14. `Q16`: how motivated to make sure have enough time to sleep, 5-point Likert Scale (1: extremely motivated, 2: very motivated, 3: somewhat motivated, 4: not that motivated, 5: not motivated at all)
15. `Q17`: how important a part of routine is going to bed at a suitable time, 5-point Likert Scale (1: extremely , 2: very important, 3: somewhat important, 4: not that important, 5: not important at all)
16. `Q22`: whether have been diagnosed sleep disorder (Yes/No)
17. `Q23`: answered only if answer for Q22 is 'Yes', what type of sleep disorder (3 choices: sleep apnea, insomnia, other sleep disorder)

I have recoded some of the variables to let the scale of extent be positive, for example: `5` mean `'the most'` and `1` mean `'the least'` for all the variables.

In the original data, `'refuse to answer'` was encoded as `-1`. In the meantime, except for the conditional questions, few missing values were present. 

```{r, warning=FALSE}
#packages 
options(warn=-1)
pkg <- c("readr","readxl","dplyr","stringr","ggplot2","tidyr","car","tidy")
pkgload <- lapply(pkg, require, character.only = TRUE)
```

```{r,warning=F}
## load data 
# Load data
#sleep = read_xlsx(file.choose())
sleep = read_xlsx("sleep.xlsx")
```

## 2.1 Data Cleaning & Variable Construction

```{r,warning=F}
tra_cat=NULL
for (i in 1:length(sleep)){
   tra_cat[i]=is.na(sleep[,i])
}
tra_cat %>% table()
for (i in 1:length(sleep)){
   tra_cat[i]=is.null(sleep[,i])
}
tra_cat %>% table()

colSums(is.na(sleep))[colSums(is.na(sleep))>0]


```

However, in particular, sleep quality does not have any missing value, so we did not filter with regards to this variable.

 After that, I created a new variable called 
       ```'sleep efficiency'```
   by dividing average actual sleep per day by average in bed hours per day. The definition of sleep efficiency is given in the *Backgroud Information* section.  

   I found that 86 participants have sleep efficiency > 1, which surprisingly tells me many people have relatively decent sleep efficiency.
   
   But do they really sleep well? Does high sleep efficiency means high sleep quality? I would like to explore.
```{r}
# average hours in bed per day
sleep$avg_bed = (sleep$DOV_WEEKTIME/ 60 * 5 + sleep$DOV_WEEKEND / 60 * 2)/ 7
# average actual sleep in hours per day
sleep$avg_actual_sleep = (sleep$DOV_TOTALWEEK/ 60 * 5 + sleep$DOV_TOTALWEEKEND / 60 * 2)/ 7
 
# Define sleep efficiency as average actual sleep per day/average sleep hours per day
sleep$sleep_efficiency = sleep$avg_actual_sleep/sleep$avg_bed
sleep$sleep_efficiency_week = sleep$DOV_TOTALWEEK/sleep$DOV_WEEKTIME
sleep$sleep_efficiency_weekend = sleep$DOV_TOTALWEEKEND/sleep$DOV_WEEKEND

sleep$sleep_efficiency[sleep$sleep_efficiency > 1] = 1
sleep$sleep_efficiency_week[sleep$sleep_efficiency_week > 1] = 1
sleep$sleep_efficiency_weekend[sleep$sleep_efficiency_weekend > 1] = 1


```
```{r}
# Whether the person go to bed before or after mid-night on weekdays
sleep$before_mnt_week = 'Before Mid-night'
sleep$before_mnt_week[sleep$Q2_ampmA == 1] = 'After Mid-night'
# Whether the person go to bed before or after mid-night on weekends
sleep$before_mnt_weekend = 'Before Mid-night'
sleep$before_mnt_weekend[sleep$Q3_ampmA == 1] = 'After Mid-night'
```


As mentioned in the last section, I reverse-coded some variables to make `5` always mean `'the most'` and `1` always mean `'the least'`. The two variables reverse coded are "Motivation to make sure you have enough time to sleep (`Q16`)" and "Importance of going to bed at a suitable time (`Q17`)". Once the reverse coding was done, `'_rev'` was added to the variable name. We noted that after the reverse coding, `'-1'` that represented `'refuse to answer'` was transformed into `'7'`. 


```{r}
# Reverse Coding
reverse_code <- function(col){
   
   return(max(col)-col + 1)
}
   
# Motivation to make sure you have enough time to sleep
sleep$Q16_rev = reverse_code(sleep$Q16)

# Importance of going to bed at a suitable time
sleep$Q17_rev = reverse_code(sleep$Q17)
```


In the original data set, for `Q22` that asked whether the participants have been diagnosed sleep disorder, `'Yes'` was encoded as `1`, and `'No'` was encoded as `2`. To make the data more intuitive, we recoded `2` to `0`. 


```{r}
# Sleep Disorders
sleep$Q22_rev = sleep$Q22
sleep$Q22_rev[sleep$Q22 == 2] = 0
```


## 2.2 Individual Variables 

### Sleep Quality

We started to look into the key variable: sleep quality (range from 1-5 as 5 being highest quality) by using the summary statistics and a count plot, and found out most people fall into the region of 3-4. 

```{r}
# Summary Statistics of Sleep Quality
t(t(sleep$Q10_a %>% summary()))


ggplot(sleep, aes(x=factor(Q10_a),fill=factor(sleep$Q10_a)))+
  geom_bar(stat="count", width=0.7)+
    ggtitle('Distribution of Sleep Quality') +
    xlab('Sleep Quality') +
    ylab('Overall Counts')
  
```

### 2.2.2 Average Hours in Bed Per Day

For average hours in bed per day, I used summary statistics and plotted a histogram with the kde distribution overlayed on it to take a look of the variable's distribution. I found out that the distribution is relatively normal, and the mean average hours in bed is 8.14 per day for the participants.


```{r}
# Summary Statistics of Average Hours in Bed Per Day
t(t(sleep$avg_bed %>% summary()))
```
```{r}
```


```{r}
ggplot(sleep, aes(x=sleep$avg_bed)) + 
    geom_histogram(aes(y=..density..),      # Histogram with density instead of count on y-axis
                   binwidth=.5,
                   colour="black", fill="white") +
    geom_density(alpha=.2, fill="#FF6666")  # Overlay with transparent density plot
```



I found that for people with very low hours in bed, more people had lower quality. At the same time, for people with high hours in bed, their ratings of sleep quality were not very different from those of the general population.  

The findings are consistent with common belief about sleep. 
```{r}
summary(sleep$avg_bed)
IQR=IQR(sleep$avg_bed,na.rm = T)
bed_Q1=7.321 
bed_outlier_lower = sleep[(sleep$avg_bed <= bed_Q1 - 1.5 * IQR),]
cat('Number of People with Very Low Hours in Bed: ' ,length(bed_outlier_lower))
print('Sleep Quality of People with Very Low Hours in Bed')
print(bed_outlier_lower$avg_bed %>% summary())
bed_outlier_upper = sleep[(sleep$avg_bed >= bed_Q1 + 1.5 * IQR),]
cat('Number of People with Very High Hours in Bed: ' , length(bed_outlier_upper))
print('Sleep Quality of People with Very High Hours in Bed')
print(t(t(bed_outlier_upper$avg_bed%>% summary())))


```

```{r,warning=F}

ggplot(bed_outlier_lower, aes(bed_outlier_lower$Q10_a,fill=factor(bed_outlier_lower$Q10_a)))+
geom_bar(stat="count", width=0.7,na.rm = T)+
    ggtitle('Distribution of Sleep Quality') +
    xlab('Sleep Quality') +
    ylab('Overall Counts')
 
ggplot(bed_outlier_upper, aes(bed_outlier_upper$Q10_a,fill=factor(bed_outlier_upper$Q10_a)))+
geom_bar(stat="count", width=0.7,na.rm = T)+
    ggtitle('Distribution of Sleep Quality') +
    xlab('Sleep Quality') +
    ylab('Overall Counts')
   
```


### 2.2.3  Sleep Efficiency


```{r}
# Summary Statistics of Sleep Efficiency

sleep$sleep_efficiency %>% summary(.,na.rm=T)
ggplot(sleep, aes(x=sleep_efficiency)) + 
    geom_histogram(aes(y=..density..),      # Histogram with density instead of count on y-axis
                   binwidth=.5,
                   colour="black", fill="white") +
    geom_density(alpha=.2, fill="#FF6666")  # Overlay with transparent density plot
```

### 2.3 Average Hours in Bed & Sleep Quality
Below are kde plots of average bedtime for five different sleep quality. While people with sleep quality from 1 to 4 have very similar kernel distributions, we found out that for people with very low sleep quality (sleep quality = 1), their sleep efficiency is more spread out.
```{r}

ggplot(sleep, aes(x=avg_bed, colour=factor(Q10_a,))) + geom_density()+
ggtitle('Sleep Quality v.s. Average Hours in Bed ')+xlab('Average Hours in Bed')

```

### 2.3.2 Average Acutal Sleep & Sleep Quality

Now, I want to study the relationship between sleep quality and average actual sleep hours. Below we divided people into three categories: short sleepers (less than 5.5 hours), moderate sleepers (5.5 - 10 hours), long sleepers (above 10 hours). 

The thresholds are defined in a paper mentioned in the *backgroud information* section and used bar plots to investivage their sleep quality. 

I found that the distributions of sleep quality for long sleepers and moderate sleepers are very similar, but the sleep quality of short sleepers concentrates on relatively lower ratings. 



```{r}
require(gridExtra)
low=sleep[sleep$avg_bed<5.5,]
mid=sleep[sleep$avg_bed<10 & sleep$avg_bed>5.5 ,]
high=sleep[sleep$avg_bed>10,]
g1=ggplot(low, aes(low$Q10_a,fill=factor(low$Q10_a)))+
geom_bar(stat="count", width=0.7,na.rm = T)+
    ggtitle('Distribution of Sleep Quality') +
    xlab('Sleep Quality') +
    ylab('Overall Counts')
g2=ggplot(mid, aes(mid$Q10_a,fill=factor(mid$Q10_a)))+
geom_bar(stat="count", width=0.7,na.rm = T)+
    ggtitle('Distribution of Sleep Quality') +
    xlab('Sleep Quality') +
    ylab('Overall Counts')
g3=ggplot(high, aes(high$Q10_a,fill=factor(high$Q10_a)))+
geom_bar(stat="count", width=0.7,na.rm = T)+
    ggtitle('Distribution of Sleep Quality') +
    xlab('Sleep Quality') +
    ylab('Overall Counts')

grid.arrange(g1,g2,g3)

```


### 2.4 Sleep Quality vs. Disorder

From the piechart, I can see that 10.8% of the participants who finished the survey have been diagnosed with sleep disorders. And the second pie chart shows among those people who have a sleep disorder, the majority, 73.7%, have Apnea.

![](https://michaelmiaomiao.github.io/img/output_67_0.png)

I found that whether or not the participants have disorder will influence their sleep quality

When I focused on people who have been diagnosed with sleep disorder, their sleep quality is relatively lower than people without disorders according to the plot below. 

```{r}
dis=sleep[sleep$Q22_rev==1,]
nodis=sleep[sleep$Q22_rev==0,]
g4=ggplot(nodis, aes(nodis$Q10_a,fill=factor(nodis$Q10_a)))+
geom_bar(stat="count", width=0.7,na.rm = T)+
    ggtitle('Distribution of Sleep Quality') +
    xlab('no disorder') +
    ylab('Overall Counts')+ theme(legend.position="top")
g5=ggplot(dis, aes(dis$Q10_a,fill=factor(dis$Q10_a)))+
geom_bar(stat="count", width=0.7,na.rm = T)+
    ggtitle('  ') +
    xlab('disorder') +
    ylab('Overall Counts')+ theme(legend.position="top")
grid.arrange(g4,g5,ncol=2)

```

### 2.5 Other Factors Correlated with Sleep Quality

Below is the correlation plot among those variables and sleep quality. We found out that "Motivation to Sleep"(r = 0.15) and "Importance of Sleep" (r = 0.13) have positive relationship with sleep quality, and other variables all have negative relationships with sleep quality. (The most negatively associated variable is "health problems").  

These findings are consistent with common belief about sleep, so I am going to incorporate these variables in our models and further investigate their relationship with sleep quality. 
```{r}

corr_data = sleep[,c('Q10_a','Q14a','Q15_a', 'Q15_b', 'Q15_c', 'Q15_d', 'Q15_e','Q16_rev', 'Q17_rev')]
colnames(corr_data) = c( 'Sleep Quality', 'Health Problems', 'Outside Noise', 'Inside Noise', 'Light','Temperature', 'Uncomfortable Mattress', 'Motivation to Sleep', 'Importance of Sleep')

# Filter out all the refused to respond
corr_data=corr_data[corr_data['Light']!=-1,]
corr_data=corr_data[corr_data['Motivation to Sleep']!=-1,]
corr_data=corr_data[corr_data['Importance of Sleep']!=-1,]
corr_data=corr_data[corr_data['Inside Noise']!=-1,]
corr_data=corr_data[corr_data['Uncomfortable Mattress']!=-1,]
corr_data=corr_data[corr_data['Health Problems']!=-1,]
corr_data=corr_data[corr_data['Motivation to Sleep']!=7,]
corr_data=corr_data[corr_data['Importance of Sleep']!=7,]

```
```{r}
library(ggcorrplot)
corr <- round(cor(corr_data), 2)
ggcorrplot(corr, hc.order = TRUE, type = "lower",
   lab = TRUE)
```


## 3.1 Linear Regression

I understand that our response variable `sleep quality` is ordinal, and by fitting a linear regression model, I would be assuming that:
 
    The response variable is continuous, which means the numerical distance between each set of subsequent categories is equal.

Such assumption would make the resulting coefficients hard to interpret and obscure the meaning of the predicted values.

However, I believe the linear regression is a nice initial start to look at the mutual relationship of all the variables with sleep quality. I first extracted and cleaned the data frame used for the linear regression. 

The data is cleaned using Python and named "new_sleep.csv" whici I will use directly

```{r}
df <- read.csv("new_sleep.csv")
df=df[,-16]
head(df,3)
```

### 3.1.1 VIF

Hence,I investigated the collinearity issue using **Variable Inflation Factor (VIF)**, and I found that sleep efficiency, average hours in bed, and average acutal sleep are highly collinear with VIF >> 5.  


```{r}
mod=lm(data = df, formula = quality~.)
car::vif(mod)
```

Hence I removed `avg_actual_sleeptime` and check agian the **VIF** which looks nice to start building full model

```{r}
mod=lm(data = df, formula = quality~.-avg_actual_sleeptime )
car::vif(mod)
```

### 3.1.1 The Full Linear Regression Model
```{r}
mod=lm(data = df, formula = quality~.-avg_actual_sleeptime )
print(mod %>% summary())
```

I found 7 of the variabls are statistically significant. 

### 3.1.2 Best Subset Variable Selection

I conducted AIC,BIC, Forward, Backward selection and concluded to use 10 variables by looking at these 4 plots graphed using plotly.
![](https://michaelmiaomiao.github.io/webfile/112.png)


According to the statistics from the best subset selection, we went one step further to fit a model with only 10 variables.  
I found that the 7 variables that had statistically significant coefficients in the full model are all kept in the model with fewer variables and are still the only variables that had statistically significant coefficients. Also, the directions of their associations with sleep quality are the same.  

So, I started to build the reduced model.

```{r}
mod=lm(data = df, formula = quality~efficiency+avg_bedtime+disorder+motivation+temperature+mattress+health+weekend_midnight+weekday_midnight+inside_noise)
print(mod %>% summary())
car::avPlots(mod)
```


## 4. Conclusion

THe data exploratory process confirmed that sleep quality is associated with sleep efficiency, average hours in bed, average actual sleep,time go to bed, sleep disorder, how motivated to make sure have enough time to sleep, and  how important a part of routine is going to bed at a suitable time, environmental factors, and health problems. 

From  the multiple linear regression model, we found that among all these variables, sleep efficiency, average hours in bed, sleep disorder, how motivated to make sure have enough time to sleep, light, uncomfortable mattrees, and  health problems, are especially significantly associated with sleep quality. 

The pattern and trends of sleep quality with respect to other factors make sense. For future study, we could try to build models like random forest, SVM, kNN, etc. to predict the quality of sleep with as multi-class classification case.

## 5. Limitations

- The data are relatively subjective and the quality of sleep is hard to measure and quantify in clinical study.

- The data has no demographic information for me to study.

>>> Jiashu Miao 11/25/2019
