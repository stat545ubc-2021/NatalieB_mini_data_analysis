---
title: "Mini Data Analysis"
author: "Natalie"
date: "08/10/2021"
output:
  html_document: default
  pdf_document: default
---

# Housekeeping tasks before beginning project

1. [x] Install the [`datateachr`](https://github.com/UBC-MDS/datateachr) package by typing the following into your **R terminal**


2. [x]Load the packages below

```{r setup, include=FALSE}
library(datateachr)
library(tidyverse)
```

3. [x] Make a repository in the https://github.com/stat545ubc-2021 Organization. You will be working with this repository for the entire data analysis project. You can either make it public, or make it private and add the TA's and Vincenzo as collaborators. 

4. [x] When you go to submit, submit a URL to your repository to canvas. 


Other:[x] load personal dataset
```{r setup, include=FALSE}
library(readr)
CTmax_swim_Fry <- read_csv("CTmax_swim_Fry.csv", 
    col_types = cols(`Fish ID` = col_character(), 
        `dropout time` = col_time(format = "%H:%M:%S"), 
        `Acclimation temp C` = col_character(), 
        `fork length (mm)` = col_double(),
        `Mass (g)`= col_double(),
        `Dropout temp` = col_double()))
        
    
                View(CTmax_swim_Fry)
```


# Task 1.1: Choose Your Favourite Datasets

1: CTmax_swim_Fry (personal dataset)

2: steam_games

3: vancouver_trees

4: parking_meters

## 1.2: Explore datasets 

This dataset has 6 columns and 122 rows; data explores temperature, time, mass, and length characteristics of Chinook fry. Temperature acclimation number is treated as character class. Also contains time as a class.

```{r}
class(CTmax_swim_Fry)
glimpse(CTmax_swim_Fry)
```


This dataset has 21 columns and 40,833 rows; the data explores game ratings, mature content warnings, developers and publishers, as well as genre, languages available, and specs required for the games to run. The majority of the data is character class.

```{r}
class(steam_games)
glimpse(steam_games)
```

This dataset has 20 columns and 146,611 rows; the data contains information regarding tree location (with street, block, neighbourhood), species, cultivar, root barrier. Most data contained in this dataset is a character class, but also contains the class "date"

```{r}
class(vancouver_trees)
glimpse(vancouver_trees)
```

This dataset contains 22 columns and 10,032 rows; the data contains information such as credit card payment (yes/no), pay by phone code, specific coordinates (longitude and latitude), neighbourhood located, and whether it is a single or twin paystation. This dataset conatins all but two rows labeled as character.

```{r}
class(parking_meters)
glimpse(parking_meters)
```
## 1.3: Narrow it down to 2


| Dataset name | Description |
| :---        |    :----:   |  
| CTmax_swim_fry| This subset of my overall data collection is interesting because it was a part of the research project that had the most unknowns about it, as this type of experiment is still quite novel. I'm interested in being able to explore more into this dataset to be able to explore results  | 
|steam_games   |   I'm interested in this dataset because I spend some time gaming, but I don't do it enough to warrant buying loads of games, so being able to have many different games with reviews, ratings, and descriptions readily available for analysis is apealing to me.    | 


## The final decison! 

|Dataset name    |Research Question |
| :---        |    :----:   |
| CTmax_swim_fry| What is the relationship between acclimation temperature and dropout temperature     | 
|steam_games   |Is there a relationship between mature content rating and overall game rating?        | 

**Final Choice :** CTmax_swim_fry


 
 
 
# Task 2: Exploring your dataset

## Introduction

This is an exploration of the dataset CTmax_swim_fry. This dataset contains critical thermal maximum data for stream-type Chinook salmon (*Oncorhynchus tshawytscha*) fry during swim flume trial experiments. 

## 2.1: complete 4 of 8 excercies / 2.2: provide a brief explanation of reasoning 
## Load required libraries for task

```{r setup, include= FALSE}
library(ggplot2)
library(ggridges)
library(scales)
library(tsibble)
library(tidyverse)
library(rlang)

```
*1. Plot the distribution of a numeric variable*

```{r}




```



*4. Explore the relationship between 2 variables*
```{r}




```



*6. Use a boxplot to look at the frequency of different observations within a single variable*
 I decided to use a boxplot to visualize the distributions of dropout temperatures given the acclimation temperature as this can give me an idea of the mean dropout temperature for each acclimation temperature, as well as the other quartiles.
```{r}

(ggplot(CTmax_swim_Fry, aes(`Acclimation temp C`,`Dropout temp` ))
 
 + geom_boxplot( aes(fill=`Acclimation temp C` )))


```



*8. Use a density plot to explore any of your variables*

```{r}




```



# Task 3: Write your research questions

##1. Is there a relationship between acclimation temperature and body mass
##2. I  
##3.
##4. 