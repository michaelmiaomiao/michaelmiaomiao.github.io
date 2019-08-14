---
layout:     post
title:      Web-browser Automation with Selenium
subtitle:   With Selenium, Python can be enabled to let users enter, search, scrape down and manipulate information from any source simply in one piece of scripts, with one click to run code and get your result. 
date:       2019-08-11
author:     Jiashu Miao
header-img: 
catalog: true
tags:
    - Python
    - Selenium
    - Numpy
    - Pandas
    - Text analytics
    - Project 
    
---
<p float="left">
    <img src="https://www.python.org/static/community_logos/python-logo.png" width="200"> 
    <img src="https://devonblog.com/wp-content/uploads/2018/08/selenium.png" width="200"> 
    <img src = "https://vcheckglobal.com//wp-content/uploads/2018/01/global-logo.png" width = "200">
    <img src = "https://jupyter.org/assets/hublogo.svg" width = "200">
</p>

This is a project from a due diligence company called [Vcheck Global](https://vcheckglobal.com/), which provides services such as background screening, document retrieval and specialized research. The objective is to achieve a stable and user-friendly algorithm to assist employess (including non-tech) to search and obtain the information with **high automation, high efficiency, preprocessing for data, and easy-to-operate features from any web sources. 

- Question to solve


### My code basically works in the following flow:
   
   - use input function to prompt searching questions to users and collect text entered.
    - interact with users to to make sure the security and accuracy.
    - call the selenium web_driver to turn on the browser, enter the information and click any neccessary button on website on behalf of users, and eventually close the browser window.
    - optimize users' searching with a dynamic algorithm if the information is not entered correctly and repeat steps to replace manual operation of the code. 
    - scrape down the raw data, preprocess the data (cleaning, imputation, tranformation, format & type etc) and create neat dataframe tables with Pandas and Numpy modules.
    - store in local with designed name automatically created based on searching information (e.g. person's name, website title, table title etc.)
    - interact with users to import the scraped information to conduct any further manipulation, analysis or evaluations. 
    - run in the backstage to save memory, and automatically turn on/off after setting the command. 


- Features:
    - run fast and can handle big-data.
    - complete automation brings user-friendly operation.
    - excellent accessibility if run on Jupyter servers.
    - secured visit to any target web sources with virtual information from selenium to protect users
    - high accuracy because of the nature to optimize entered information and interactions with users.
