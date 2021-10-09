# Housekeeping tasks before beginning project

1.  [x] Install the
    [`datateachr`](https://github.com/UBC-MDS/datateachr) package by
    typing the following into your **R terminal**

2.  [x] Load the packages below

``` r
library(datateachr)
library(tidyverse)
```

1.  [x] Make a repository in the <https://github.com/stat545ubc-2021>
    Organization. You will be working with this repository for the
    entire data analysis project. You can either make it public, or make
    it private and add the TA’s and Vincenzo as collaborators.

2.  [x] When you go to submit, submit a URL to your repository to
    canvas.

-   [x] Load personal dataset

``` r
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

This dataset has 6 columns and 122 rows; data explores temperature,
time, mass, and length characteristics of Chinook fry. Temperature
acclimation number is treated as character class. Also contains time as
a class.

``` r
class(CTmax_swim_Fry)
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

``` r
glimpse(CTmax_swim_Fry)
```

    ## Rows: 121
    ## Columns: 6
    ## $ `Fish ID`            <chr> "1", "2", "3", "4", "5", "6", "7", "8", "9", "10"~
    ## $ `Dropout temp`       <dbl> 27.2, 27.9, 28.0, 28.0, 28.0, 28.0, 28.0, 28.0, 2~
    ## $ `dropout time`       <time> 04:51:26, 05:02:28, 05:04:03, 05:05:04, 05:05:38~
    ## $ `fork length (mm)`   <dbl> 49, 47, 37, 38, 42, 41, 39, 44, 41, 41, 45, 41, 4~
    ## $ `Mass (g)`           <dbl> 1.04, 0.93, 0.57, 0.51, 0.68, 0.65, 0.50, 0.76, 0~
    ## $ `Acclimation temp C` <chr> "15", "15", "15", "15", "15", "15", "15", "15", "~

This dataset has 21 columns and 40,833 rows; the data explores game
ratings, mature content warnings, developers and publishers, as well as
genre, languages available, and specs required for the games to run. The
majority of the data is character class.

``` r
class(steam_games)
```

    ## [1] "spec_tbl_df" "tbl_df"      "tbl"         "data.frame"

``` r
glimpse(steam_games)
```

    ## Rows: 40,833
    ## Columns: 21
    ## $ id                       <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14~
    ## $ url                      <chr> "https://store.steampowered.com/app/379720/DO~
    ## $ types                    <chr> "app", "app", "app", "app", "app", "bundle", ~
    ## $ name                     <chr> "DOOM", "PLAYERUNKNOWN'S BATTLEGROUNDS", "BAT~
    ## $ desc_snippet             <chr> "Now includes all three premium DLC packs (Un~
    ## $ recent_reviews           <chr> "Very Positive,(554),- 89% of the 554 user re~
    ## $ all_reviews              <chr> "Very Positive,(42,550),- 92% of the 42,550 u~
    ## $ release_date             <chr> "May 12, 2016", "Dec 21, 2017", "Apr 24, 2018~
    ## $ developer                <chr> "id Software", "PUBG Corporation", "Harebrain~
    ## $ publisher                <chr> "Bethesda Softworks,Bethesda Softworks", "PUB~
    ## $ popular_tags             <chr> "FPS,Gore,Action,Demons,Shooter,First-Person,~
    ## $ game_details             <chr> "Single-player,Multi-player,Co-op,Steam Achie~
    ## $ languages                <chr> "English,French,Italian,German,Spanish - Spai~
    ## $ achievements             <dbl> 54, 37, 128, NA, NA, NA, 51, 55, 34, 43, 72, ~
    ## $ genre                    <chr> "Action", "Action,Adventure,Massively Multipl~
    ## $ game_description         <chr> "About This Game Developed by id software, th~
    ## $ mature_content           <chr> NA, "Mature Content Description  The develope~
    ## $ minimum_requirements     <chr> "Minimum:,OS:,Windows 7/8.1/10 (64-bit versio~
    ## $ recommended_requirements <chr> "Recommended:,OS:,Windows 7/8.1/10 (64-bit ve~
    ## $ original_price           <dbl> 19.99, 29.99, 39.99, 44.99, 0.00, NA, 59.99, ~
    ## $ discount_price           <dbl> 14.99, NA, NA, NA, NA, 35.18, 70.42, 17.58, N~

This dataset has 20 columns and 146,611 rows; the data contains
information regarding tree location (with street, block, neighbourhood),
species, cultivar, root barrier. Most data contained in this dataset is
a character class, but also contains the class “date”

``` r
class(vancouver_trees)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

``` r
glimpse(vancouver_trees)
```

    ## Rows: 146,611
    ## Columns: 20
    ## $ tree_id            <dbl> 149556, 149563, 149579, 149590, 149604, 149616, 149~
    ## $ civic_number       <dbl> 494, 450, 4994, 858, 5032, 585, 4909, 4925, 4969, 7~
    ## $ std_street         <chr> "W 58TH AV", "W 58TH AV", "WINDSOR ST", "E 39TH AV"~
    ## $ genus_name         <chr> "ULMUS", "ZELKOVA", "STYRAX", "FRAXINUS", "ACER", "~
    ## $ species_name       <chr> "AMERICANA", "SERRATA", "JAPONICA", "AMERICANA", "C~
    ## $ cultivar_name      <chr> "BRANDON", NA, NA, "AUTUMN APPLAUSE", NA, "CHANTICL~
    ## $ common_name        <chr> "BRANDON ELM", "JAPANESE ZELKOVA", "JAPANESE SNOWBE~
    ## $ assigned           <chr> "N", "N", "N", "Y", "N", "N", "N", "N", "N", "N", "~
    ## $ root_barrier       <chr> "N", "N", "N", "N", "N", "N", "N", "N", "N", "N", "~
    ## $ plant_area         <chr> "N", "N", "4", "4", "4", "B", "6", "6", "3", "3", "~
    ## $ on_street_block    <dbl> 400, 400, 4900, 800, 5000, 500, 4900, 4900, 4900, 7~
    ## $ on_street          <chr> "W 58TH AV", "W 58TH AV", "WINDSOR ST", "E 39TH AV"~
    ## $ neighbourhood_name <chr> "MARPOLE", "MARPOLE", "KENSINGTON-CEDAR COTTAGE", "~
    ## $ street_side_name   <chr> "EVEN", "EVEN", "EVEN", "EVEN", "EVEN", "ODD", "ODD~
    ## $ height_range_id    <dbl> 2, 4, 3, 4, 2, 2, 3, 3, 2, 2, 2, 5, 3, 2, 2, 2, 2, ~
    ## $ diameter           <dbl> 10.00, 10.00, 4.00, 18.00, 9.00, 5.00, 15.00, 14.00~
    ## $ curb               <chr> "N", "N", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "Y", "~
    ## $ date_planted       <date> 1999-01-13, 1996-05-31, 1993-11-22, 1996-04-29, 19~
    ## $ longitude          <dbl> -123.1161, -123.1147, -123.0846, -123.0870, -123.08~
    ## $ latitude           <dbl> 49.21776, 49.21776, 49.23938, 49.23469, 49.23894, 4~

This dataset contains 22 columns and 10,032 rows; the data contains
information such as credit card payment (yes/no), pay by phone code,
specific coordinates (longitude and latitude), neighbourhood located,
and whether it is a single or twin paystation. This dataset conatins all
but two rows labeled as character.

``` r
class(parking_meters)
```

    ## [1] "tbl_df"     "tbl"        "data.frame"

``` r
glimpse(parking_meters)
```

    ## Rows: 10,032
    ## Columns: 22
    ## $ meter_head     <chr> "Twin", "Pay Station", "Twin", "Single", "Twin", "Twin"~
    ## $ r_mf_9a_6p     <chr> "$2.00", "$1.00", "$1.00", "$1.00", "$2.00", "$2.00", "~
    ## $ r_mf_6p_10     <chr> "$4.00", "$1.00", "$1.00", "$1.00", "$1.00", "$1.00", "~
    ## $ r_sa_9a_6p     <chr> "$2.00", "$1.00", "$1.00", "$1.00", "$2.00", "$2.00", "~
    ## $ r_sa_6p_10     <chr> "$4.00", "$1.00", "$1.00", "$1.00", "$1.00", "$1.00", "~
    ## $ r_su_9a_6p     <chr> "$2.00", "$1.00", "$1.00", "$1.00", "$2.00", "$2.00", "~
    ## $ r_su_6p_10     <chr> "$4.00", "$1.00", "$1.00", "$1.00", "$1.00", "$1.00", "~
    ## $ rate_misc      <chr> NA, "$ .50", NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA~
    ## $ time_in_effect <chr> "METER IN EFFECT: 9:00 AM TO 10:00 PM", "METER IN EFFEC~
    ## $ t_mf_9a_6p     <chr> "2 Hr", "10 Hrs", "2 Hr", "2 Hr", "2 Hr", "3 Hr", "2 Hr~
    ## $ t_mf_6p_10     <chr> "4 Hr", "10 Hrs", "4 Hr", "4 Hr", "4 Hr", "4 Hr", "4 Hr~
    ## $ t_sa_9a_6p     <chr> "2 Hr", "10 Hrs", "2 Hr", "2 Hr", "2 Hr", "3 Hr", "2 Hr~
    ## $ t_sa_6p_10     <chr> "4 Hr", "10 Hrs", "4 Hr", "4 Hr", "4 Hr", "4 Hr", "4 Hr~
    ## $ t_su_9a_6p     <chr> "2 Hr", "10 Hrs", "2 Hr", "2 Hr", "2 Hr", "3 Hr", "2 Hr~
    ## $ t_su_6p_10     <chr> "4 Hr", "10 Hrs", "4 Hr", "4 Hr", "4 Hr", "4 Hr", "4 Hr~
    ## $ time_misc      <chr> NA, "No Time Limit", NA, NA, NA, NA, NA, NA, NA, NA, NA~
    ## $ credit_card    <chr> "No", "Yes", "No", "No", "No", "No", "No", "No", "No", ~
    ## $ pay_phone      <chr> "66890", "59916", "57042", "57159", "51104", "60868", "~
    ## $ longitude      <dbl> -123.1289, -123.0982, -123.1013, -123.1862, -123.1278, ~
    ## $ latitude       <dbl> 49.28690, 49.27215, 49.25468, 49.26341, 49.26354, 49.27~
    ## $ geo_local_area <chr> "West End", "Strathcona", "Riley Park", "West Point Gre~
    ## $ meter_id       <chr> "670805", "471405", "C80145", "D03704", "301023", "5913~

## 1.3: Narrow it down to 2

| Dataset name   |                                                                                                                                        Description                                                                                                                                        |
|:---------------|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
| CTmax_swim_fry | This subset of my overall data collection is interesting because it was a part of the research project that had the most unknowns about it, as this type of experiment is still quite novel. I’m interested in being able to explore more into this dataset to be able to explore results |
| steam_games    |             I’m interested in this dataset because I spend some time gaming, but I don’t do it enough to warrant buying loads of games, so being able to have many different games with reviews, ratings, and descriptions readily available for analysis is apealing to me.              |

## The final decison!

| Dataset name   |                                Research Question                                 |
|:---------------|:--------------------------------------------------------------------------------:|
| CTmax_swim_fry | What is the relationship between acclimation temperature and dropout temperature |
| steam_games    |  Is there a relationship between mature content rating and overall game rating?  |

**Final Choice :** CTmax_swim_fry

# Task 2: Exploring your dataset

## Introduction

This is an exploration of the dataset CTmax_swim_fry. This dataset
contains critical thermal maximum data for stream-type Chinook salmon
(*Oncorhynchus tshawytscha*) fry during swim flume trial experiments.

## 2.1: complete 4 of 8 excercies / 2.2: provide a brief explanation of reasoning

## Load required libraries for task

``` r
library(ggplot2)
library(ggridges)
library(scales)
library(tsibble)
library(tidyverse)
library(rlang)
```

## *1. Plot the distribution of a numeric variable*

I would like to look at body mass distribution; was there a proportion
of fish body types that are over-represented in the data?
Under-represented?

``` r
(ggplot(CTmax_swim_Fry, aes(`Mass (g)`))
 +geom_density()
 +ylab("distribution of fish mass (g)"))
```

![](mini-data-analysis-deliverable-1_files/figure-markdown_github/unnamed-chunk-8-1.png)

## *4. Explore the relationship between 2 variables*

I decided to look at the relationship between body mass and dropout
time, as I’m curious to see if longer-bodied fish were able for a longer
period of time; I chose to visualize this by using a scatter plot, to
see if there are specific groupings that emerge.

``` r
(ggplot(CTmax_swim_Fry, aes(`fork length (mm)`, `dropout time`))+
   geom_point( aes(colour= `fork length (mm)`) )) 
```

![](mini-data-analysis-deliverable-1_files/figure-markdown_github/unnamed-chunk-9-1.png)

## *6. Use a boxplot to look at the frequency of different observations within a single variable*

I decided to use a boxplot to visualize the distributions of dropout
temperatures given the acclimation temperature as this can give me an
idea of the mean dropout temperature for each acclimation temperature,
as well as the other quartiles.

``` r
(ggplot(CTmax_swim_Fry, aes(`Acclimation temp C`,`Dropout temp` ))
 
 + geom_boxplot( aes(fill=`Acclimation temp C` )))
```

![](mini-data-analysis-deliverable-1_files/figure-markdown_github/unnamed-chunk-10-1.png)

## *8. Use a density plot to explore any of your variables*

# Task 3: Write your research questions

**1. Is there a relationship between acclimation temperature and body
mass**

**2. Is there a relationship between dropout temperature and acclimation
temperature**

**3. Is There a relationship between fork length and dropout time**

**4. Is there a relationship between body mass and dropout temperature**
