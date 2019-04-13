Milestone 3 - Final Report
================
Rayce Rossum, Alex Hope, Tina Pan, Krish Andivel
April 12, 2019

Question
--------

As students in MDS who are completing their degree, we were curious about the experience of our classmates over the course of the program. There is a general consensus that the two toughest blocks (4 courses per block) of month long material were covered in January and February, which were blocks 4 and 5. While both were considered difficult they were quite different in educational content.

Block 4 contained coursework on extensive concepts in machine learning, ranging from ML algorithms, deep learning, feature and model selection, regularization, among other topics generally taught within the computing science department. On the other hand, Block 5 contained statistics courses covering regression, time-series/spatial statistics, and Bayesian statistics.

Our interest in this experiment was to consider the background of students, and the role this played in their perception of the more difficult block (4 or 5). The background we chose to explore in our survey contained the following questions: Educational Background (Faculty) of last degree, Field/Major, Occupational History (last job held), Age, Sex (Male or Female or Prefer Not to Say), and Block Difficulty (Which was harder? 4 or 5?).

Our hypothesis is that students with a statistics/math/life science background (education or occupation) will rate the machine learning block (Block-4) as the harder block, whereas students with a computer-science background (education or occupation) will rate the statistics block (Block-5) as the more difficult one. We believe there is a relationship between educational focus, occupational history and efficacy in school, and that this can be measured by individual perceptions of difficulty using our outcome question.

Methods
-------

-   Tina \#\# Survey Study Design
-   Rayce \#\# Data Collection Methods
-   Survey
-   Manual binning of free text categoricals \#\# Analysis Methods
-   All TODO \#\# Results and Analysis
-   TODO \#\# Discussion of Results
-   TODO \#\# Discussion of your Survey/Study design
-   Discuss possible burnout factors and time factors
-   Perhaps next time we assess difficulty after each block individually, rather than relying on retrospective memory of participants

### Data

``` r
# import packages
library(tidyverse)
```

    ## -- Attaching packages -------------------------------------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.1.0       v purrr   0.3.0  
    ## v tibble  2.0.1       v dplyr   0.8.0.1
    ## v tidyr   0.8.2       v stringr 1.3.1  
    ## v readr   1.3.1       v forcats 0.3.0

    ## -- Conflicts ----------------------------------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(dplyr)
```

``` r
# import data
data <- read.csv("../data/data.csv") 

data <- data %>% 
  
  mutate(
    
    # DV - binary: 0 - block 4 harder; 1 - block 5 harder
    Y = ifelse(Which.block.did.you.find.more.difficult. == "Block 4 (January)", 0, 1),
    
    sex = ifelse(What.is.your.sex. == "Male", "M", "F")) %>%
  
  select(faculty = Faculty,
         
         age = Which.age.group.do.you.belong.to.,
         
         last_job = Last_Job.Categorical.,
         
         sex,
         
         Y)

data$faculty <- factor(data$faculty)
# faculty = 1: Science
# faculty = 2: Business
# faculty = 3: Engineering
# faculty = 4: Arts

data$last_job <- factor(data$last_job)
# last_job = 0: No working experience
# last_job = 1: Science
# last_job = 2: Business
# last_job = 3: Engineering
# last_job = 9: Other

data$sex<- factor(data$sex)

summary(data)
```

    ##  faculty    age     last_job sex          Y         
    ##  1:26    19-24:16   0: 5     F:26   Min.   :0.0000  
    ##  2:10    25-29:26   1:20     M:32   1st Qu.:0.0000  
    ##  3:17    30-34: 9   2:23            Median :1.0000  
    ##  4: 5    35+  : 7   3: 3            Mean   :0.5862  
    ##                     9: 7            3rd Qu.:1.0000  
    ##                                     Max.   :1.0000

Logistic Regression Analysis
----------------------------

### model 1: 1 IV (only faculty)

First, fit the simple logistic regression model with just one IV (`faculty`):

``` r
# model 1: 1 IV (only faculty)
mod1 <- glm(Y ~ faculty, data = data, family = "binomial")
summary(mod1)
```

    ## 
    ## Call:
    ## glm(formula = Y ~ faculty, family = "binomial", data = data)
    ## 
    ## Deviance Residuals: 
    ##    Min      1Q  Median      3Q     Max  
    ## -1.354  -1.312   1.011   1.044   1.049  
    ## 
    ## Coefficients:
    ##             Estimate Std. Error z value Pr(>|z|)
    ## (Intercept)  0.31015    0.39696   0.781    0.435
    ## faculty2     0.09531    0.75779   0.126    0.900
    ## faculty3     0.04652    0.63280   0.074    0.941
    ## faculty4     0.09531    0.99544   0.096    0.924
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 78.672  on 57  degrees of freedom
    ## Residual deviance: 78.651  on 54  degrees of freedom
    ## AIC: 86.651
    ## 
    ## Number of Fisher Scoring iterations: 4

-   Since all of the p-values are larger than 0.05, we don't have siginificant evidence to show any of the faculty class is siginificant to determine the perception of block difficulty.

-   The intercept of 0.31015 is the log odds for `faculty1` to find block 5 harder since it is the reference group.

-   The coefficient for `faculty2` is the difference of log of odds ratio between the `faculty2` group and `faculty1` group, which is 0.09531. Similarly, we can interpret the corresponding coefficients for `faculty3` and `faculty4`.

### model 2: 2 IV (faculty and last\_job) without interaction term

From EDA, we find last\_job might be the other IV, then we add it to our logistic regression model and no interaction term:

``` r
# model 2: 2 IV (faculty and last_job) without interaction term
mod2 <- glm(Y ~ faculty + last_job, data = data, family = "binomial")
summary(mod2)
```

    ## 
    ## Call:
    ## glm(formula = Y ~ faculty + last_job, family = "binomial", data = data)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.7526  -1.1329   0.6963   0.9763   1.3618  
    ## 
    ## Coefficients:
    ##              Estimate Std. Error z value Pr(>|z|)
    ## (Intercept)    1.2458     1.1515   1.082    0.279
    ## faculty2       0.2326     0.8239   0.282    0.778
    ## faculty3       0.3766     0.7619   0.494    0.621
    ## faculty4       0.4669     1.0506   0.444    0.657
    ## last_job1     -0.3291     1.2417  -0.265    0.791
    ## last_job2     -1.3514     1.2257  -1.103    0.270
    ## last_job3    -18.1885  1385.3783  -0.013    0.990
    ## last_job9     -1.6694     1.4089  -1.185    0.236
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 78.672  on 57  degrees of freedom
    ## Residual deviance: 68.511  on 50  degrees of freedom
    ## AIC: 84.511
    ## 
    ## Number of Fisher Scoring iterations: 15

-   Since all of the p-values are larger than 0.05, we don't have siginificant evidence to show any of the faculty or last\_job class is siginificant to determine the perception of block difficulty.

-   The intercept of 1.2458 is the log odds for `faculty1` and `last_job0` to find block 5 harder since it is the reference group.

-   The coefficient for `faculty2` is the difference of log of odds ratio between the `faculty2` group and `faculty1` group holding the same `last_job` group, which is 0.2326. Similarly, we can intepret corresponding coefficients for `faculty3` and `faculty4`.

-   The coefficient for `last_job1` is the difference of log of odds ratio between the `last_job1` group and `last_job0` group holding the same `faculty` group, which is -0.3291. Similarly, we can intepret the corresponding coefficients for `last_job2`, `last_job3` and `last_job9`.

#### Chi-square deviance test - Comparision of `model 1` and `model 2`

``` r
anova(mod1, mod2, test="Chisq")
```

    ## Analysis of Deviance Table
    ## 
    ## Model 1: Y ~ faculty
    ## Model 2: Y ~ faculty + last_job
    ##   Resid. Df Resid. Dev Df Deviance Pr(>Chi)  
    ## 1        54     78.651                       
    ## 2        50     68.511  4    10.14  0.03813 *
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

-   The result shows a Df of 4, indicating that the more complex model (`model 2`) has 4 additional parameter.

-   Since p-value &lt; 0.05, adding the IV `last_job` to the model does lead to a significantly improved fit over the `model 1`.

### model 3: 2 IV (faculty and last\_job) with interaction term

``` r
# model 3: 2 IV (faculty and last_job) with interaction term
mod3 <- glm(Y ~ faculty * last_job, data = data, family = "binomial")
summary(mod3)
```

    ## 
    ## Call:
    ## glm(formula = Y ~ faculty * last_job, family = "binomial", data = data)
    ## 
    ## Deviance Residuals: 
    ##     Min       1Q   Median       3Q      Max  
    ## -1.7344  -1.0842   0.7090   0.9832   1.3537  
    ## 
    ## Coefficients: (7 not defined because of singularities)
    ##                     Estimate Std. Error z value Pr(>|z|)
    ## (Intercept)           0.6931     1.2247   0.566    0.571
    ## faculty2              0.5108     1.0165   0.503    0.615
    ## faculty3             16.8729  2797.4422   0.006    0.995
    ## faculty4              0.4055     1.6833   0.241    0.810
    ## last_job1             0.5596     1.4639   0.382    0.702
    ## last_job2            -0.9163     1.3964  -0.656    0.512
    ## last_job3           -35.1321  3611.4820  -0.010    0.992
    ## last_job9            -1.0986     1.5275  -0.719    0.472
    ## faculty2:last_job1   -1.0704     1.7822  -0.601    0.548
    ## faculty3:last_job1  -17.2094  2797.4424  -0.006    0.995
    ## faculty4:last_job1   15.9078  3956.1808   0.004    0.997
    ## faculty2:last_job2        NA         NA      NA       NA
    ## faculty3:last_job2  -16.2443  2797.4424  -0.006    0.995
    ## faculty4:last_job2   -0.1823     2.2986  -0.079    0.937
    ## faculty2:last_job3        NA         NA      NA       NA
    ## faculty3:last_job3        NA         NA      NA       NA
    ## faculty4:last_job3        NA         NA      NA       NA
    ## faculty2:last_job9        NA         NA      NA       NA
    ## faculty3:last_job9        NA         NA      NA       NA
    ## faculty4:last_job9        NA         NA      NA       NA
    ## 
    ## (Dispersion parameter for binomial family taken to be 1)
    ## 
    ##     Null deviance: 78.672  on 57  degrees of freedom
    ## Residual deviance: 66.480  on 45  degrees of freedom
    ## AIC: 92.48
    ## 
    ## Number of Fisher Scoring iterations: 16

-   Since all of the p-values are larger than 0.05, we don't have siginificant evidence to show any of class or interaction term is siginificant to determine the perception of block difficulty.

-   The intercept of 0.6931 is the log odds for `faculty1` and `last_job0` group to find block 5 harder since it is the reference group.

-   The coefficient for `faculty2` is the difference of log of odds ratio between the `faculty2` group and `faculty1` group for the `last_job0` group, which is 0.5108. Similarly, we can intepret corresponding coefficients for `faculty3` and `faculty4`.

-   The coefficient for `last_job1` is the difference of log of odds ratio between the `last_job1` group and `last_job0` group for the `faculty1` group, which is 0.5596. Similarly, we can intepret the corresponding coefficients for `last_job2`, `last_job3` and `last_job9`.

-   The coefficient for `faculty2:last_job1` is the difference is the difference between the log-odds ratio comparing `faculty2` vs `faculty1` in `last_job1` and the log-odds ratio comparing `faculty2` vs `faculty1` in `last_job0`. Similarly, we can intepret the corresponding coefficients for the other interaction terms.

#### Chi-square deviance test - Comparision of `model 2` and `model 3`

``` r
anova(mod2, mod3, test="Chisq")
```

    ## Analysis of Deviance Table
    ## 
    ## Model 1: Y ~ faculty + last_job
    ## Model 2: Y ~ faculty * last_job
    ##   Resid. Df Resid. Dev Df Deviance Pr(>Chi)
    ## 1        50     68.511                     
    ## 2        45     66.480  5   2.0305   0.8449

-   The result shows a Df of 5, indicating that the more complex model (`model 3`) has 5 additional parameter.

-   Since p-value &gt; 0.05, adding the interaction term to the model does NOT lead to a significantly improved fit over the `model 2`.
