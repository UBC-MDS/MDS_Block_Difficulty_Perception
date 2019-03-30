## Perceived Block Difficulty in MDS

> Identify the question that your team is in interested in answering with the survey. The aim of the survey should be to try to answer one specific and testable question. Examples of specific and testable questions include (you can use one of these if you really like them):


Question: **Does an MDS student's educational background influence their perception of block difficulty?**

To explore this question, we'll collect educational background (IV) information and attitudes towards the block difficulty (DV) in the survey. Since block #4 and #5 were considered the two most stressful blocks for us, and included overarching themes in data science and statistics, we will ask the respondent to select the harder block, which will be the perception data for our analysis.

> Identify the other questions you plan to ask in your survey to identify confounding variables and justify/explain why you plan to include them.

Other questions we plan to ask in our survey include:

  - What was your last job?
    - Non-educational experience can make certain blocks easier or harder.
      - Ex. A respondent who has an unrelated degree but worked in bio-statistics will find block 4 harder.
    - This variable is confounding as a respondent's job experience may influence their ability in different areas. 
    
  - Which age group do you belong to?
    - Age and life experience can influence a respondents comfort with different topics.
      - Ex. An older respondent may have a more difficult time working with computers and therefore will find block 4 harder.
    - This variable is confounding as a respondent's age may inluence their comfort in different areas. 
    
  - What is your sex?
    - Sex could influence a respondent's preference to learning certain material.
      - Ex. Men prefer the rigorous math of statistics whereas women prefer the elegance of machine learning.
    - This variable is confounding as a respondent's sex may influence their preference towards different areas.

> Describe how you plan to analyze the survey results (e.g., what statistical test(s) do you plan to employ?)

The purpose of our experiment is to understand whether different educational backgrounds (IV) are related to perceived block difficulty (DV) of students in MDS. Our educational background variable (IV) is comprised of multiple levels (ex. business, life sciences, comp sci, stats/math, engineering) and perceived block difficulty is a binary outcome where respondents pick the harder block between #4 and #5.

We will utilize a logistic regression model to assess the association between our IV and DV and consider potential confounding variables associated with both our IV and DV in the ensuing analysis as well.

> Discuss the aspects of the UBC Office of Research Ethics document on Using Online Surveys that are relevant to your proposed survey.


RESPONSE HERE

