---
layout:     post
title:      HopSkipDrive Driver Marketplace Analysis 
subtitle:   A marketplace analysis for 27k data of suppliers & customers, including cohort analysis, concentration, take rate, conversation rate, power usrs etc. using Excel and R.
date:       2019-09-16
author:     Jiashu Miao
header-img: 
catalog: true
tags:
    - R
    - Excel
    - Google Sheet
    - cohort analysis
    - marketplace 
    
---

### For demo and recruiters view only, please do not repost or disclose any data & information.

## Background

This is a data project comes from HopSkipDrive for interview challenge: HopSkipDrive has always been dedicated to making a difference in the lives of children and families. We understand that transportation can be the difference between success and struggle, which is why we’re on a mission to use technology, operational expertise, and new thinking to help kids reach their full potential by providing a safe, dependable way to get them where they need to be.  [Source](https://www.hopskipdrive.com/about)

## Overview 

I had 2 hours to complete the exercise. I should bias toward showing my work (e.g. don’t delete calculations) and imagine me creating a model that will be used over and over again by you and the team (i.e. that fresh data could be dumped into the model without having to redo the modeling).  

Note: imagine that the data in the flatfile was pulled on January 1, 2019 and is limited to events that registered in 2018 - i.e. it is likely that drivers on that list have had and will have events in 2019 that are not captured here.

## Questions: 

- Early driver lifecycle

1. What is average and median number of days from when a driver is activated that it takes her to complete 5, 10, 15, 20, 25 and 30 trips?

2. What percent of drivers complete 30 trips within their first x days after being activated?  Where x is a dynamic assumption that you or a user could change without changing any formuals. 

3. Set x at the number of days you think we should use to approximate conversion rate - i.e. to answer the question: "what percent of drivers that we activate will likely ever complete 30 trips?"

- Driver productivity

1. How many casual drivers and how many power drivers do we currently have living in each metro area and overall?   Decide on your own definition of power vs. casual driver and make those criteria flexible - i.e. so that you or a user of your model could later change the definition without changing formulas.   

2. Which cohort of drivers had the highest percentage of power drivers?  Where a cohort is defined by a group of drivers activated in the same month. 

3. BONUS (if time): Create the capability for a user of your model to flexibly strip specific zipcodes out of the analysis - e.g. for any user to decide they want to see answers to the questions above without anywhere from 1-10 zipcodes being included in the analsyis.  The user should be able to set these zipcodes dynamically without changing any formulas or manually manipulating the data. 

- Observations & Insights

1. Three observations you have about driver behavior from the analysis you conducted.

2. Three questions about driver behavior you would want answered from the data if you had more time and/or another dataset to merge with this one.
