---
layout:     post
title:      Validation of XML Files using R
subtitle:   How does R enable automatic XML files validation and error log collection 
date:       2020-10-29
author:     Jiashu Miao
header-img: 
header-style: text
catalog: true
tags:

    - R
    - Data Science 
    - Bigdata
    - Jupyter
    - Python
    
---

## Introduction
- R could be an useful language not only to conduct statistical analysis but complete some functional jobs at fast speed with little human interference.
- The XML validation is a process that R could handle perfectly and even works better than many paid business softwares.
- It is extremely flexible and could automate the process and operate for multiple files simultaneously. 



---
title: "Untitled"
author: "JIASHU MIAO"
date: "2/6/2020"
output: html_document
---

```{r}
library(dplyr)
library(magrittr)
```

```{r}
sum(is.na(c(2,3
        )))
```
```{r}
# install.packages("xml2")

doc <- xml2::read_xml(file.choose())
schema <- xml2::read_xml(file.choose())
```
```{r}
xml2::xml_validate(doc,schema)
validation <- xml2::xml_validate(doc,schema)
```


```{r}

print(attr(validation,"errors"))
```

```{r}
one <- mtcars[1:4, ]
two <- mtcars[11:14, ]
list(one,two)
# You can supply data frames as arguments:



# The contents of lists is automatically spliced:
identical(bind_rows(one, two),bind_rows(list(one, two)))

bind_rows(list(one, two), list(two, one))






```
