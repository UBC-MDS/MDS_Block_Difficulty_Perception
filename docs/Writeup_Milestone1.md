## Perceived Block Difficulty in MDS

> Identify the question that your team is in interested in answering with the survey. The aim of the survey should be to try to answer one specific and testable question. Examples of specific and testable questions include (you can use one of these if you really like them):


Question: **Does an MDS student's educational background influence their perception of block difficulty?**

To explore this question, we'll collect educational background (IV) information and attitudes towards the block difficulty (DV) in the survey. Since block #4 and #5 were considered the two most stressful blocks for students, and included overarching themes in machine learning and statistics, we will ask the respondent to select the harder block, which will be the perception data for our analysis.

> Identify the other questions you plan to ask in your survey to identify confounding variables and justify/explain why you plan to include them.

Other questions we plan to ask in our survey include:

  - What was your last job?
    - Non-educational experience can make certain blocks easier or harder.
      - Ex. A respondent who has an unrelated degree but worked in bio-statistics will find block 4 harder.
    - This variable is confounding as a respondent's job experience may influence their experience in different areas. 
    
  - Which age group do you belong to?
    - Age and life experience can influence a respondents comfort with different topics.
      - Ex. An older respondent may have a more difficult time working with computers and therefore will find block 4 harder.
    - This variable is confounding as a respondent's age may influence their comfort in different areas. 
    
  - What is your sex?
    - Sex could influence a respondent's preference to learning certain material.
      - Ex. Men prefer the rigorous math of statistics whereas women prefer the elegance of machine learning.
    - This variable is confounding as a respondent's sex may influence their preference towards different areas.

> Describe how you plan to analyze the survey results (e.g., what statistical test(s) do you plan to employ?)

The purpose of our experiment is to understand whether different educational backgrounds (IV) are related to perceived block difficulty (DV) of students in MDS. Our educational background variable (IV) is comprised of multiple levels (ex. business, life sciences, comp sci, stats/math, engineering) and perceived block difficulty is a binary outcome where respondents pick the harder block between #4 and #5.

We will first fit a logistic regression model using the education background as the predictor variable and the arrival time as the response variable. We will use log odds ratio to determine association of education background to the block 4/5 which is the response variable.  The odds ratio can be any non-negative number. An odds ratio of 1 serves as the base for comparison which indicates there is no association between the response and predictor. We will choose block 4 of the response variable as the reference. Separate odds ratios will be determined for block 5, except for the reference. The odds ratios then represent the change in odds of the outcome being a block 5 versus the block4, for differing factor levels of the predictor variable.
We will utilize a logistic regression model to assess the association between our IV and DV and consider potential confounding variables associated with both our IV and DV in the ensuing analysis as well.

> Discuss the aspects of the UBC Office of Research Ethics document on Using Online Surveys that are relevant to your proposed survey.

Under FIPPA (Freedom of Information and Protection and Privacy Act), personal information is considered both direct (DOB, SIN #, etc.) and indirect identifiers (postal code, date of birth) or other unique questions that may identify individuals in a small sample. In the context of our study, the only potential direct identifier would be the "last job" question for a few individuals in the cohort who had a unique past occupation. However, this really depends on the level of specificity the participant chooses to provide. With this in mind, we intend to take any precautions necessary to protect individuals if identifiable information is exposed. We will anonymize the data where necessary and ask for consent prior to the study onset as well.

