Milestone 3 - Final Report
================
Rayce Rossum, Alex Hope, Tina Pan, Krish Andivel
April 12, 2019

Question
--------

As students in MDS who are completing their degree, we were curious about the experience of our classmates over the course of the program. There is a general consensus that the two toughest blocks (4 courses per block) of month long material were covered in January and February, which were blocks 4 and 5. While both were considered difficult they were quite different in educational content.

Block 4 contained coursework on extensive concepts in machine learning, ranging from ML algorithms, deep learning, feature and model selection, regularization, among other topics generally taught within the computing science department. On the other hand, Block 5 contained statistics courses covering regression, time-series/spatial statistics, and Bayesian statistics.

Our interest in this experiment was to consider the background of students, and the role this played in their perception of the more difficult block (4 or 5).

Our hypothesis is that students with a statistics/math/life science background (education or occupation) will rate the machine learning block (Block-4) as the harder block, whereas students with a computer-science background (education or occupation) will rate the statistics block (Block-5) as the more difficult one. We believe there is a relationship between educational focus, occupational history and efficacy in school, and that this can be measured by individual perceptions of difficulty using our outcome question.

Methods
-------

### Survey Study Design

Our survey was designed with six questions we used to gauge a persons background, as well as their perception of whether block 4 or block 5 was more difficult.

The included questions were:

##### Which faculty is your undergraduate degree from?

-   This question was categorical including options such as "business" and "science" with the option to add a faculty if we happened to miss one.
-   We designed this question to deduce whether experience in one faculty will contribute to more experience in statistics or computer science which would ultimately contribute to perception of difficulty.

##### What is your undergraduate major?

-   This question was a free text field which we manually binned.
-   We designed this question to differentiate between computer science majors and statistics majors who both fall under the "science" faculty.

##### What was your last job?

-   This question was a free text field which we manually binned.
-   We designed this question to deduce whether past work experience contributed to the difficulty of block perception.

##### Which age group do you belong to?

-   This question was categorical with options in 5 year age groups from 19 - 35+.
-   We designed to deduce whether or not age was a confounding factor in choice of undergraduate degree or last job.

##### What is your sex?

-   This question was categorical with options including "Female", "Male" and "Prefer not to say".
-   We designed to deduce whether or not sex was a confounding factor in choice of undergraduate degree or last job.

##### Which block did you find more difficult?

-   This question was binary with the choices of either block 4 or block 5.
-   This was our response variable.

### Data Collection Methods

-   Survey
-   Manual binning of free text categoricals

<table>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
faculty
</th>
<th style="text-align:left;">
    age </th>

<th style="text-align:left;">
last\_job
</th>
<th style="text-align:left;">
sex
</th>
<th style="text-align:left;">
       Y </th>

</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
1:26
</td>
<td style="text-align:left;">
19-24:16
</td>
<td style="text-align:left;">
0: 5
</td>
<td style="text-align:left;">
F:26
</td>
<td style="text-align:left;">
Min. :0.0000
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
2:10
</td>
<td style="text-align:left;">
25-29:26
</td>
<td style="text-align:left;">
1:20
</td>
<td style="text-align:left;">
M:32
</td>
<td style="text-align:left;">
1st Qu.:0.0000
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
3:17
</td>
<td style="text-align:left;">
30-34: 9
</td>
<td style="text-align:left;">
2:23
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
Median :1.0000
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
4: 5
</td>
<td style="text-align:left;">
35+ : 7
</td>
<td style="text-align:left;">
3: 3
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
Mean :0.5862
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
9: 7
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
3rd Qu.:1.0000
</td>
</tr>
<tr>
<td style="text-align:left;">
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
NA
</td>
<td style="text-align:left;">
Max. :1.0000
</td>
</tr>
</tbody>
</table>
> faculty = 1: Science <br> faculty = 2: Business <br> faculty = 3: Engineering <br> faculty = 4: Arts <br> <br> last\_job = 0: Unemployed or N/A <br> last\_job = 1: Science <br> last\_job = 2: Business <br> last\_job = 3: Engineering <br> last\_job = 9: Arts

Analysis Methods
----------------

-   TODO:

Results and Analysis
--------------------

### EDA

![](../img/EDA_1.png) We can find the overall distribution for each variable from histograms of `Faculty`, `Block_Difficulty`, `Age` and `Sex` above.

![](../img/EDA_2.png)

![](../img/EDA_3.png)

When looking at the `Block_Difficulty` for each group of `Faculty` and `Last_job`, it shows that `Faculty` doesn't affect `Block_Difficulty` much, but `Last_job` does.

### Model 1: 1 IV (only faculty)

First, fit the simple logistic regression model with just one IV (`faculty`):

``` r
# model 1: 1 IV (only faculty)
mod1 <- glm(Y ~ faculty, data = data, family = "binomial")
kable(tidy(mod1))
```

<table>
<thead>
<tr>
<th style="text-align:left;">
term
</th>
<th style="text-align:right;">
estimate
</th>
<th style="text-align:right;">
std.error
</th>
<th style="text-align:right;">
statistic
</th>
<th style="text-align:right;">
p.value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
(Intercept)
</td>
<td style="text-align:right;">
0.3101549
</td>
<td style="text-align:right;">
0.3969581
</td>
<td style="text-align:right;">
0.7813291
</td>
<td style="text-align:right;">
0.4346090
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty2
</td>
<td style="text-align:right;">
0.0953102
</td>
<td style="text-align:right;">
0.7577878
</td>
<td style="text-align:right;">
0.1257742
</td>
<td style="text-align:right;">
0.8999106
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty3
</td>
<td style="text-align:right;">
0.0465200
</td>
<td style="text-align:right;">
0.6327977
</td>
<td style="text-align:right;">
0.0735148
</td>
<td style="text-align:right;">
0.9413964
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty4
</td>
<td style="text-align:right;">
0.0953102
</td>
<td style="text-align:right;">
0.9954442
</td>
<td style="text-align:right;">
0.0957464
</td>
<td style="text-align:right;">
0.9237220
</td>
</tr>
</tbody>
</table>
-   Since all of the p-values are larger than 0.05, we don't have siginificant evidence to show any of the faculty class is siginificant to determine the perception of block difficulty.

-   The intercept of 0.31015 is the log odds for `faculty1` to find block 5 harder since it is the reference group.

-   The coefficient for `faculty2` is the difference of log of odds ratio between the `faculty2` group and `faculty1` group, which is 0.09531. Similarly, we can interpret the corresponding coefficients for `faculty3` and `faculty4`.

### Model 2: 2 IV (`faculty` and `last_job`) without Interaction Terms

From EDA, we found last\_job might be another IV, therefore we test that by adding it to our logistic regression model using no interaction terms:

``` r
# model 2: 2 IV (faculty and last_job) without interaction term
mod2 <- glm(Y ~ faculty + last_job, data = data, family = "binomial")
kable(tidy(mod2))
```

<table>
<thead>
<tr>
<th style="text-align:left;">
term
</th>
<th style="text-align:right;">
estimate
</th>
<th style="text-align:right;">
std.error
</th>
<th style="text-align:right;">
statistic
</th>
<th style="text-align:right;">
p.value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
(Intercept)
</td>
<td style="text-align:right;">
1.2458271
</td>
<td style="text-align:right;">
1.1515021
</td>
<td style="text-align:right;">
1.0819147
</td>
<td style="text-align:right;">
0.2792904
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty2
</td>
<td style="text-align:right;">
0.2325512
</td>
<td style="text-align:right;">
0.8239055
</td>
<td style="text-align:right;">
0.2822547
</td>
<td style="text-align:right;">
0.7777482
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty3
</td>
<td style="text-align:right;">
0.3766393
</td>
<td style="text-align:right;">
0.7619206
</td>
<td style="text-align:right;">
0.4943289
</td>
<td style="text-align:right;">
0.6210739
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty4
</td>
<td style="text-align:right;">
0.4669496
</td>
<td style="text-align:right;">
1.0506338
</td>
<td style="text-align:right;">
0.4444456
</td>
<td style="text-align:right;">
0.6567204
</td>
</tr>
<tr>
<td style="text-align:left;">
last\_job1
</td>
<td style="text-align:right;">
-0.3291284
</td>
<td style="text-align:right;">
1.2417223
</td>
<td style="text-align:right;">
-0.2650580
</td>
<td style="text-align:right;">
0.7909648
</td>
</tr>
<tr>
<td style="text-align:left;">
last\_job2
</td>
<td style="text-align:right;">
-1.3514203
</td>
<td style="text-align:right;">
1.2256691
</td>
<td style="text-align:right;">
-1.1025980
</td>
<td style="text-align:right;">
0.2702018
</td>
</tr>
<tr>
<td style="text-align:left;">
last\_job3
</td>
<td style="text-align:right;">
-18.1885348
</td>
<td style="text-align:right;">
1385.3783327
</td>
<td style="text-align:right;">
-0.0131289
</td>
<td style="text-align:right;">
0.9895249
</td>
</tr>
<tr>
<td style="text-align:left;">
last\_job9
</td>
<td style="text-align:right;">
-1.6693973
</td>
<td style="text-align:right;">
1.4088512
</td>
<td style="text-align:right;">
-1.1849351
</td>
<td style="text-align:right;">
0.2360431
</td>
</tr>
</tbody>
</table>
-   Since all of the p-values are larger than 0.05, we don't have siginificant evidence to show any of the faculty or last\_job class is siginificant to determine the perception of block difficulty.

-   The intercept of 1.2458 is the log odds for `faculty1` and `last_job0` of finding block 5 harder since it is the reference group.

-   The coefficient for `faculty2` is the difference of log of odds ratio between the `faculty2` group and `faculty1` group holding the same `last_job` group, which is 0.2326. Similarly, we can intepret corresponding coefficients for `faculty3` and `faculty4`.

-   The coefficient for `last_job1` is the difference of log of odds ratio between the `last_job1` group and `last_job0` group holding the same `faculty` group, which is -0.3291. Similarly, we can intepret the corresponding coefficients for `last_job2`, `last_job3` and `last_job9`.

### Chi-square Deviance Test - Comparison of `model 1` and `model 2`

``` r
kable(tidy(anova(mod1, mod2, test="Chisq")))
```

<table>
<thead>
<tr>
<th style="text-align:right;">
Resid..Df
</th>
<th style="text-align:right;">
Resid..Dev
</th>
<th style="text-align:right;">
df
</th>
<th style="text-align:right;">
Deviance
</th>
<th style="text-align:right;">
p.value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
54
</td>
<td style="text-align:right;">
78.65098
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
</tr>
<tr>
<td style="text-align:right;">
50
</td>
<td style="text-align:right;">
68.51053
</td>
<td style="text-align:right;">
4
</td>
<td style="text-align:right;">
10.14044
</td>
<td style="text-align:right;">
0.0381272
</td>
</tr>
</tbody>
</table>
-   The result shows a Df of 4, indicating that the more complex model (`model 2`) has 4 additional parameters.

-   Since p-value &lt; 0.05, adding the IV `last_job` to the model does lead to a significantly improved fit over the `model 1`.

### Model 3: 2 IV (`faculty` and `last_job`) with Interaction Terms

``` r
# model 3: 2 IV (faculty and last_job) with interaction term
mod3 <- glm(Y ~ faculty * last_job, data = data, family = "binomial")
kable(tidy(mod3))
```

<table>
<thead>
<tr>
<th style="text-align:left;">
term
</th>
<th style="text-align:right;">
estimate
</th>
<th style="text-align:right;">
std.error
</th>
<th style="text-align:right;">
statistic
</th>
<th style="text-align:right;">
p.value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
(Intercept)
</td>
<td style="text-align:right;">
0.6931472
</td>
<td style="text-align:right;">
1.224745
</td>
<td style="text-align:right;">
0.5659523
</td>
<td style="text-align:right;">
0.5714262
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty2
</td>
<td style="text-align:right;">
0.5108256
</td>
<td style="text-align:right;">
1.016530
</td>
<td style="text-align:right;">
0.5025190
</td>
<td style="text-align:right;">
0.6153025
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty3
</td>
<td style="text-align:right;">
16.8729213
</td>
<td style="text-align:right;">
2797.442206
</td>
<td style="text-align:right;">
0.0060316
</td>
<td style="text-align:right;">
0.9951875
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty4
</td>
<td style="text-align:right;">
0.4054651
</td>
<td style="text-align:right;">
1.683251
</td>
<td style="text-align:right;">
0.2408822
</td>
<td style="text-align:right;">
0.8096464
</td>
</tr>
<tr>
<td style="text-align:left;">
last\_job1
</td>
<td style="text-align:right;">
0.5596158
</td>
<td style="text-align:right;">
1.463850
</td>
<td style="text-align:right;">
0.3822904
</td>
<td style="text-align:right;">
0.7022460
</td>
</tr>
<tr>
<td style="text-align:left;">
last\_job2
</td>
<td style="text-align:right;">
-0.9162907
</td>
<td style="text-align:right;">
1.396424
</td>
<td style="text-align:right;">
-0.6561694
</td>
<td style="text-align:right;">
0.5117151
</td>
</tr>
<tr>
<td style="text-align:left;">
last\_job3
</td>
<td style="text-align:right;">
-35.1321370
</td>
<td style="text-align:right;">
3611.482013
</td>
<td style="text-align:right;">
-0.0097279
</td>
<td style="text-align:right;">
0.9922384
</td>
</tr>
<tr>
<td style="text-align:left;">
last\_job9
</td>
<td style="text-align:right;">
-1.0986123
</td>
<td style="text-align:right;">
1.527525
</td>
<td style="text-align:right;">
-0.7192106
</td>
<td style="text-align:right;">
0.4720112
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty2:last\_job1
</td>
<td style="text-align:right;">
-1.0704414
</td>
<td style="text-align:right;">
1.782187
</td>
<td style="text-align:right;">
-0.6006336
</td>
<td style="text-align:right;">
0.5480840
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty3:last\_job1
</td>
<td style="text-align:right;">
-17.2093935
</td>
<td style="text-align:right;">
2797.442447
</td>
<td style="text-align:right;">
-0.0061518
</td>
<td style="text-align:right;">
0.9950916
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty4:last\_job1
</td>
<td style="text-align:right;">
15.9078404
</td>
<td style="text-align:right;">
3956.180767
</td>
<td style="text-align:right;">
0.0040210
</td>
<td style="text-align:right;">
0.9967917
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty3:last\_job2
</td>
<td style="text-align:right;">
-16.2443126
</td>
<td style="text-align:right;">
2797.442436
</td>
<td style="text-align:right;">
-0.0058068
</td>
<td style="text-align:right;">
0.9953668
</td>
</tr>
<tr>
<td style="text-align:left;">
faculty4:last\_job2
</td>
<td style="text-align:right;">
-0.1823216
</td>
<td style="text-align:right;">
2.298550
</td>
<td style="text-align:right;">
-0.0793202
</td>
<td style="text-align:right;">
0.9367779
</td>
</tr>
</tbody>
</table>
-   Since all of the p-values are larger than 0.05, we don't have siginificant evidence to show any of class or interaction term is siginificant to determine the perception of block difficulty.

-   The intercept of 0.6931 is the log odds for `faculty1` and `last_job0` group to find block 5 harder since it is the reference group.

-   The coefficient for `faculty2` is the difference of log of odds ratio between the `faculty2` group and `faculty1` group for the `last_job0` group, which is 0.5108. Similarly, we can intepret corresponding coefficients for `faculty3` and `faculty4`.

-   The coefficient for `last_job1` is the difference of log of odds ratio between the `last_job1` group and `last_job0` group for the `faculty1` group, which is 0.5596. Similarly, we can intepret the corresponding coefficients for `last_job2`, `last_job3` and `last_job9`.

-   The coefficient for `faculty2:last_job1` is the difference is the difference between the log-odds ratio comparing `faculty2` vs `faculty1` in `last_job1` and the log-odds ratio comparing `faculty2` vs `faculty1` in `last_job0`. Similarly, we can intepret the corresponding coefficients for the other interaction terms.

### Chi-square Deviance Test - Comparison of `model 2` and `model 3`

``` r
kable(tidy(anova(mod2, mod3, test="Chisq")))
```

<table>
<thead>
<tr>
<th style="text-align:right;">
Resid..Df
</th>
<th style="text-align:right;">
Resid..Dev
</th>
<th style="text-align:right;">
df
</th>
<th style="text-align:right;">
Deviance
</th>
<th style="text-align:right;">
p.value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;">
50
</td>
<td style="text-align:right;">
68.51053
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
<td style="text-align:right;">
NA
</td>
</tr>
<tr>
<td style="text-align:right;">
45
</td>
<td style="text-align:right;">
66.48009
</td>
<td style="text-align:right;">
5
</td>
<td style="text-align:right;">
2.030446
</td>
<td style="text-align:right;">
0.8449164
</td>
</tr>
</tbody>
</table>
-   The result shows a Df of 5, indicating that the more complex model (`model 3`) has 5 additional parameters.

-   Since p-value &gt; 0.05, adding the interaction term to the model does NOT lead to a significantly improved fit over the `model 2`.

Discussion of Results
---------------------

TODO: We found that none of the variables are relevant to the perception of block difficult.

Discussion of your Survey/Study design
--------------------------------------

-   Discuss possible burnout factors and time factors
-   Perhaps next time we assess difficulty after each block individually, rather than relying on retrospective memory of participants
