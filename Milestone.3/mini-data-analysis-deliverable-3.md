mini-data-analysis-deliverable-3
================
Natalie
27/10/2021

# Welcome to your last milestone in your mini data analysis project!

In Milestone 1, you explored your data and came up with research
questions. In Milestone 2, you obtained some results by making summary
tables and graphs.

In this (3rd) milestone, you’ll be sharpening some of the results you
obtained from your previous milestone by:

-   Manipulating special data types in R: factors and/or dates and
    times.
-   Fitting a model object to your data, and extract a result.
-   Reading and writing data as separate files.

**NOTE**: The main purpose of the mini data analysis is to integrate
what you learn in class in an analysis. Although each milestone provides
a framework for you to conduct your analysis, it’s possible that you
might find the instructions too rigid for your data set. If this is the
case, you may deviate from the instructions – just make sure you’re
demonstrating a wide range of tools and techniques taught in this class.

## Instructions

**To complete this milestone**, edit [this very `.Rmd`
file](https://raw.githubusercontent.com/UBC-STAT/stat545.stat.ubc.ca/master/content/mini-project/mini-project-3.Rmd)
directly. Fill in the sections that are tagged with
`<!--- start your work here--->`.

**To submit this milestone**, make sure to knit this `.Rmd` file to an
`.md` file by changing the YAML output settings from
`output: html_document` to `output: github_document`. Commit and push
all of your work to your mini-analysis GitHub repository, and tag a
release on GitHub. Then, submit a link to your tagged release on canvas.

**Points**: This milestone is worth 40 points (compared to the usual 30
points): 30 for your analysis, and 10 for your entire mini-analysis
GitHub repository. Details follow.

**Research Questions**: In Milestone 2, you chose two research questions
to focus on. Wherever realistic, your work in this milestone should
relate to these research questions whenever we ask for justification
behind your work. In the case that some tasks in this milestone don’t
align well with one of your research questions, feel free to discuss
your results in the context of a different research question.

# Setup

Begin by loading your data and the tidyverse package below:

``` r
library(datateachr) 
library(tidyverse)
library(broom)
library(ggplot2)
library(ggridges)
library(scales)
library(tsibble)
library(tidyverse)
library(rlang)
library(dplyr)
```

**Load personal dataset for project**

``` r
library(readr)
CTmax_swim_Fry <- read_csv("../CTmax_swim_Fry.csv", 
    col_types = cols(`Fish ID` = col_character(),
        `dropout time` = col_time(format = "%H:%M:%S"), 
        `Acclimation temp C` = col_character(), 
        `fork length (mm)` = col_double(),
        `Mass (g)`= col_double(),
        `Dropout temp` = col_double()))
View(CTmax_swim_Fry)
```

From Milestone 2, you chose two research questions. What were they? Put
them here.

<!-------------------------- Start your work below ---------------------------->

1.  *Is body mass influenced by acclimation temperature?*
2.  *Which acclimation temperature yielded fish with the highest thermal
    tolerance?*
    <!----------------------------------------------------------------------------->

# Exercise 1: Special Data Types (10)

For this exercise, you’ll be choosing two of the three tasks below –
both tasks that you choose are worth 5 points each.

But first, tasks 1 and 2 below ask you to modify a plot you made in a
previous milestone. The plot you choose should involve plotting across
at least three groups (whether by facetting, or using an aesthetic like
colour). Place this plot below (you’re allowed to modify the plot if
you’d like). If you don’t have such a plot, you’ll need to make one.
Place the code for your plot below.

**Initial plot**
<!-------------------------- Start your work below ---------------------------->

``` r
ggplot(CTmax_swim_Fry, aes(`Acclimation temp C`, `Mass (g)`))+
  geom_boxplot(aes(fill=`Acclimation temp C` ))+
  geom_jitter(aes(),
            size = 1.5,
            alpha = 0.3)+
  theme(legend.position = "none") 
```

![](mini-data-analysis-deliverable-3_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

<!----------------------------------------------------------------------------->

Now, choose two of the following tasks.

1.  Produce a new plot that reorders a factor in your original plot,
    using the `forcats` package (3 points). Then, in a sentence or two,
    briefly explain why you chose this ordering (1 point here for
    demonstrating understanding of the reordering, and 1 point for
    demonstrating some justification for the reordering, which could be
    subtle or speculative.)

2.  Produce a new plot that groups some factor levels together into an
    “other” category (or something similar), using the `forcats` package
    (3 points). Then, in a sentence or two, briefly explain why you
    chose this grouping (1 point here for demonstrating understanding of
    the grouping, and 1 point for demonstrating some justification for
    the grouping, which could be subtle or speculative.)

3.  If your data has some sort of time-based column like a date (but
    something more granular than just a year):

    1.  Make a new column that uses a function from the `lubridate` or
        `tsibble` package to modify your original time-based column. (3
        points)
        -   Note that you might first have to *make* a time-based column
            using a function like `ymd()`, but this doesn’t count.
        -   Examples of something you might do here: extract the day of
            the year from a date, or extract the weekday, or let 24
            hours elapse on your dates.
    2.  Then, in a sentence or two, explain how your new column might be
        useful in exploring a research question. (1 point for
        demonstrating understanding of the function you used, and 1
        point for your justification, which could be subtle or
        speculative).
        -   For example, you could say something like “Investigating the
            day of the week might be insightful because penguins don’t
            work on weekends, and so may respond differently”.

<!-------------------------- Start your work below ---------------------------->

**Task Number: 1**

I’ve decided to reorder the plots out of order of acclimation and place
the 24C acclimation treatment to the front. This reordering will help
with the comparison between the distribution of mass between the 15C and
24C acclimation temperatures. By using fct\_relevel(), I can manually
reorder my acclimation treatments so that 24C is in front.

Here I can see that the 24C acclimation treatment yields a much lower
body mass than the 15C more clearly.

``` r
(ggplot(CTmax_swim_Fry, aes(fct_relevel(`Acclimation temp C`, "24"), `Mass (g)`))+
  geom_boxplot(aes(fill=`Acclimation temp C` ))+
  geom_jitter(aes(),
            size = 1.5,
            alpha = 0.3)+
  theme(legend.position = "none")+
  labs(x = "Acclimation temperature"))
```

![](mini-data-analysis-deliverable-3_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

<!----------------------------------------------------------------------------->
<!-------------------------- Start your work below ---------------------------->

**Task Number: 2**

By condensing the two lowest temperature acclimations and the two
highest temperature acclimations together into two separate categories
labeled “cool” and “warm” I’m able to ascertain a bigger picture of the
effects of temperature on mass. 15C and 18C are known in literature to
be generally well-tolerated by Chinook salmon, while 20C and 24C have
been noted as approaching near-lethal temperatures.

What we can infer with the wide array of mass measurements in the “warm”
category is that acclimation temperature is acting as a chronic
selective force; some fish were better able to recruit thermal coping
strategies over time in the warm category, while others weren’t. This
variance in coping with the thermal stressor will influence their
ability to compete for food.

This isn’t seen in the “cool” temperature category is that these fish
are not being selected for thermal coping strategies, as they are not
under thermal stress. Because of this, all the fish are able to a
similar degree use their energy for growth and maintenance.

``` r
Acclimation_condensed<- CTmax_swim_Fry %>% 
    select(-`dropout time`,-`fork length (mm)`,-`Dropout temp`)%>%
    mutate(`Acclimation temp C` = fct_collapse(`Acclimation temp C`, Cool= c("15", "18") , Warm= c("20", "24")))

 ggplot(Acclimation_condensed, aes(`Acclimation temp C`, `Mass (g)`))+
  geom_boxplot(aes(fill=`Acclimation temp C` ))+
  geom_jitter(aes(),
            size = 1.5,
            alpha = 0.3)+
  theme(legend.position = "none") 
```

![](mini-data-analysis-deliverable-3_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

<!----------------------------------------------------------------------------->

# Exercise 2: Modelling

## 2.0 (no points)

Pick a research question, and pick a variable of interest (we’ll call it
“Y”) that’s relevant to the research question. Indicate these.

<!-------------------------- Start your work below ---------------------------->

**Research Question: *Is body mass influenced by acclimation
temperature?***

**Variable of interest: Mass (g)**

<!----------------------------------------------------------------------------->

## 2.1 (5 points)

Fit a model or run a hypothesis test that provides insight on this
variable with respect to the research question. Store the model object
as a variable, and print its output to screen. We’ll omit having to
justify your choice, because we don’t expect you to know about model
specifics in STAT 545.

-   **Note**: It’s OK if you don’t know how these models/tests work.
    Here are some examples of things you can do here, but the sky’s the
    limit.
    -   You could fit a model that makes predictions on Y using another
        variable, by using the `lm()` function.
    -   You could test whether the mean of Y equals 0 using `t.test()`,
        or maybe the mean across two groups are different using
        `t.test()`, or maybe the mean across multiple groups are
        different using `anova()` (you may have to pivot your data for
        the latter two).
    -   You could use `lm()` to test for significance of regression.

<!-------------------------- Start your work below ---------------------------->

I decided to do a one-way ANOVA to try and ascertain the level of
significance between the means of mass for each acclimation treatment.

``` r
(CT_max_anova <- aov(`Mass (g)` ~ `Acclimation temp C`, CTmax_swim_Fry))
```

    ## Call:
    ##    aov(formula = `Mass (g)` ~ `Acclimation temp C`, data = CTmax_swim_Fry)
    ## 
    ## Terms:
    ##                 `Acclimation temp C` Residuals
    ## Sum of Squares              3.499870  4.150127
    ## Deg. of Freedom                    3       116
    ## 
    ## Residual standard error: 0.189148
    ## Estimated effects may be unbalanced
    ## 1 observation deleted due to missingness

<!----------------------------------------------------------------------------->

## 2.2 (5 points)

Produce something relevant from your fitted model: either predictions on
Y, or a single value like a regression coefficient or a p-value.

-   Be sure to indicate in writing what you chose to produce.
-   Your code should either output a tibble (in which case you should
    indicate the column that contains the thing you’re looking for), or
    the thing you’re looking for itself.
-   Obtain your results using the `broom` package if possible. If your
    model is not compatible with the broom function you’re needing, then
    you can obtain your results by some other means, but first indicate
    which broom function is not compatible.

<!-------------------------- Start your work below ---------------------------->

Here I decided to look at the p-value, which is found in column 6, row
1. This p-value is less than 0.05, showing that there is significance in
the difference of some mean mass between acclimation temperature
treatments.

``` r
tidy(CT_max_anova)
```

    ## # A tibble: 2 x 6
    ##   term                    df sumsq meansq statistic   p.value
    ##   <chr>                <dbl> <dbl>  <dbl>     <dbl>     <dbl>
    ## 1 `Acclimation temp C`     3  3.50 1.17        32.6  2.33e-15
    ## 2 Residuals              116  4.15 0.0358      NA   NA

<!----------------------------------------------------------------------------->

# Exercise 3: Reading and writing data

Get set up for this exercise by making a folder called `output` in the
top level of your project folder / repository. You’ll be saving things
there.

## 3.1 (5 points)

Take a summary table that you made from Milestone 2 (Exercise 1.2), and
write it as a csv file in your `output` folder. Use the `here::here()`
function.

-   **Robustness criteria**: You should be able to move your Mini
    Project repository / project folder to some other location on your
    computer, or move this very Rmd file to another location within your
    project repository / folder, and your code should still work.
-   **Reproducibility criteria**: You should be able to delete the csv
    file, and remake it simply by knitting this Rmd file.

<!-------------------------- Start your work below ---------------------------->

Here I am using the tibble with the data for the median mass per
acclimation treatment

``` r
(body_mass_median <- CTmax_swim_Fry %>%
  group_by( `Acclimation temp C`) %>%
  summarise(body_mass_median = median(`Mass (g)`, na.rm = TRUE)))
```

    ## # A tibble: 5 x 2
    ##   `Acclimation temp C` body_mass_median
    ##   <chr>                           <dbl>
    ## 1 15                              0.69 
    ## 2 18                              0.81 
    ## 3 20                              0.885
    ## 4 24                              0.415
    ## 5 n/a                            NA

``` r
(write_csv(body_mass_median, here::here("output", "body_mass_median.csv")))
```

    ## # A tibble: 5 x 2
    ##   `Acclimation temp C` body_mass_median
    ##   <chr>                           <dbl>
    ## 1 15                              0.69 
    ## 2 18                              0.81 
    ## 3 20                              0.885
    ## 4 24                              0.415
    ## 5 n/a                            NA

<!----------------------------------------------------------------------------->

## 3.2 (5 points)

Write your model object from Exercise 2 to an R binary file (an RDS),
and load it again. Be sure to save the binary file in your `output`
folder. Use the functions `saveRDS()` and `readRDS()`.

-   The same robustness and reproducibility criteria as in 3.1 apply
    here.

<!-------------------------- Start your work below ---------------------------->

``` r
saveRDS(CT_max_anova, here::here("Output", "CT_max_anova.rds"))
```

``` r
CT_max_anova_printMe<- readRDS(here::here("Output", "CT_max_anova.rds"))
```

``` r
print(CT_max_anova_printMe)
```

    ## Call:
    ##    aov(formula = `Mass (g)` ~ `Acclimation temp C`, data = CTmax_swim_Fry)
    ## 
    ## Terms:
    ##                 `Acclimation temp C` Residuals
    ## Sum of Squares              3.499870  4.150127
    ## Deg. of Freedom                    3       116
    ## 
    ## Residual standard error: 0.189148
    ## Estimated effects may be unbalanced
    ## 1 observation deleted due to missingness

<!----------------------------------------------------------------------------->

# Tidy Repository

Now that this is your last milestone, your entire project repository
should be organized. Here are the criteria we’re looking for.

## Main README (3 points)

There should be a file named `README.md` at the top level of your
repository. Its contents should automatically appear when you visit the
repository on GitHub.

Minimum contents of the README file:

-   In a sentence or two, explains what this repository is, so that
    future-you or someone else stumbling on your repository can be
    oriented to the repository.
-   In a sentence or two (or more??), briefly explains how to engage
    with the repository. You can assume the person reading knows the
    material from STAT 545A. Basically, if a visitor to your repository
    wants to explore your project, what should they know?

Once you get in the habit of making README files, and seeing more README
files in other projects, you’ll wonder how you ever got by without them!
They are tremendously helpful.

## File and Folder structure (3 points)

You should have at least four folders in the top level of your
repository: one for each milestone, and one output folder. If there are
any other folders, these are explained in the main README.

Each milestone document is contained in its respective folder, and
nowhere else.

Every level-1 folder (that is, the ones stored in the top level, like
“Milestone1” and “output”) has a `README` file, explaining in a sentence
or two what is in the folder, in plain language (it’s enough to say
something like “This folder contains the source for Milestone 1”).

## Output (2 points)

All output is recent and relevant:

-   All Rmd files have been `knit`ted to their output, and all data
    files saved from Exercise 3 above appear in the `output` folder.
-   All of these output files are up-to-date – that is, they haven’t
    fallen behind after the source (Rmd) files have been updated.
-   There should be no relic output files. For example, if you were
    knitting an Rmd to html, but then changed the output to be only a
    markdown file, then the html file is a relic and should be deleted.

Our recommendation: delete all output files, and re-knit each
milestone’s Rmd file, so that everything is up to date and relevant.

PS: there’s a way where you can run all project code using a single
command, instead of clicking “knit” three times. More on this in STAT
545B!

## Error-free code (1 point)

This Milestone 3 document knits error-free. (We’ve already graded this
aspect for Milestone 1 and 2)

## Tagged release (1 point)

You’ve tagged a release for Milestone 3. (We’ve already graded this
aspect for Milestone 1 and 2)
