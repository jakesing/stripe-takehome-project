# Stripe Takehome Writeup
## Executive Summary

- Identified 1,330 target merchants in Software and Business Services
- Estimated subscription volume lift: $2.4M - $24M in first year
- Key factors: industry (Software, Business Services), country (USA, Japan), long tenure
- Recommendation: Launch targeted marketing campaign to these 1,330 merchants
- Next step: Refine ROI calculations for more precise impact estimates

## Summary
This document represents my writeup for the Stripe Data Analyst takehome assignment. The assignment was to identify a list of merchants that the sales and/or marketing teams could target in an effort to increase adoption of the Subscriptions product.

The result is a list of 1,330 merchants spanning two industries (Software and Business Services), two countries (USA and Japan), and with long-tenures with Stripe. 

Using historical performance of merchants who’ve already adopted subscriptions, the subscription volume lift of targeting these merchants is estimated to be between $2.4M and $24M in the first year. 
## Approach
Althrough the approach was data driven, it started with a vision for the ideal marketing campaign to drive adoption for subscriptions. In real life, this would be a conversation with the Head of Product and the Marketing teams involved to learn what has worked, what hasn’t, and what we already know about our customers. In the absence of this information, I leaned on my previous experience with B2B marketing, where case studies and showing impact are typically important. The starting point was therefore a desire to identify merchants who’ve achieved some important benefit from adopting subscriptions, and then identify merchants who might realize similar benefits.
I thought through the various benefits of subscriptions, and although there are several, the most important to any B2B is that it could increase revenue. 
### Starting Approach
I settled on a starting approach:
- Identify merchants who’ve adopted subscriptions during this timeframe
- Calculate their increase in revenue from before adopting subscriptions to after. 
- Label anyone who meets certain criteria as ‘successful’
- Identify their key characteristics
- Identify non-adopting merchants who share these characteristics
As I got into the analysis, I encountered a few critical problems:
- The dataset timeframe was short (just about 1 year). This caused an issue where the number of merchants who had meaningful data both before and after adopting subscriptions was low (167).
- Given this small sample, it was hard to identify meaningful unique characteristics. For example, the country distribution in the ‘successful’ set was very similar to the overall distribution of the larger sample. Additionally, 95% of the ‘successful’ merchants were classed as ‘small’. 
- Using what characteristics did appear to stand out, I only found another 165 merchants to target who matched this criteria. 
Given these issues, it occured to me that either the dataset was not conducive to this type fo analysis, my criteria for defining success was too strict, or both, and after tinkering with the criteria without much success, I concluded that this analysis was a bad fit for this dataset. I switched course.
### Revised Approach
Rather than focusing on identifying merchants who I could predict would be successful, I decided to focus on merchants that I could predict had a high likelihood of adopting subscriptions. Under this approach, we
- I ran a logistic regression with the dependant variable being a binary on ‘adopted subscriptions’.
- I identified the most important features that were associated with higher likelihoods of adoption
- I used these features to identify merchants who have not yet adopted subscriptions
This analysis yielded a larger set of target merchants (1330) and I felt more confident about these findings. I therefore moved to an estimation of the impact we might expect from targeting these merchants, and assessed the lift in subscription volume to be between $2.4M and $24M in the first year.
## Methodology
In the interest of space, I’ll focus on the methodology for the revised, final approach that is reflected in the final merchants list. To identify target merchants for increased subscription adoption, I followed these key steps:

1. Data cleaning and preparation
2. Logistic regression to identify adoption factors
3. Target merchant identification based on model insights
4. ROI estimation using historical data and assumptions

Each step provided crucial insights, culminating in our final recommendations.
### Data Cleaning
I investigated the overall structure of the data, and identified the need to clean a few things up. More details are in the Jupyter notebook in markdown blocks. The high level:
- Divided the numeric columns in the payments table by 100
- Made sure the date fields in both tables had datetime values only
- Cast the merchant (both) and industry (merchants) columns to string, as each had some non-string values
- Joined the tables and cleared rows associated with merchants with id of “0”
- Performed date validations (ensuring that the date range is as we expected, and that the first_charge_date reconciled with actual charge data)
### Propensity Model / Logistic Regression
The goal in this step was to identify what features of a merchant are most impactful in assessing likelihood of adopting subscriptions.
- The first step was to structure the data:
  - Aggregate data by merchants: summing up volume columns, taking the last value for categorical colums, and the first value for first_charge_date
  - Create dummy variables for the categorical columns
  - Filter out industries and countries outside the top 10 (by total volume) to make it easier to analyze (I saw earlier in the analysis that the top 10 represented 84% and 73% by country and industry respectively)
- Next I plotted the various variables relative to the outcome variable to get a visual representation of their relationships. See [[Stripe Takehome Writeup/Visualizations of Relationship Between Features and Outcome Variable]]
- Based on this, I had a sense of the important features, and put those into a logistic regression model
  - I used an iterative approach, where in the first attempt all previously identified features were included, and in the second attempt, only features with p-values below 0.05 were included
- The final result was a model with reasoable accuracy (0.66) and AUC score (0.70), and which identified 7 qualities that had positive effects on the likelihood of adopting subscriptions:
  - Industry
    - Software
    - Business Services
  - Country
    - US
    - Japan
  - Other features
    - Tenure: Long-term or established (I created these categories based on days since first charge)
    - Volume: high
- While these metrics indicate a moderately effective model, there's room for improvement. This performance level should be considered when interpreting our predictions and recommendations.
### Finding Targets
Using these criteria, I queried the aggregated merchants table to identify any merchant who fits the criteria above. I included 6 out of the 7, excluding only is_high_volume since it had a large negative effect on the target list. 
This result yielded:
![](Stripe%20Takehome%20Writeup/CleanShot%202024-09-26%20at%2010.29.35.png)
### ROI Analysis
I wanted to understand what might happen if we target these merchants and some of them converted to using subscriptions. To do this I needed to assume the following:
- Conversion rates: low, medium, and high conversion rates to create three scenarios
- Revenue lift: each merchant who converts will achieve the average daily subscription volume that ‘adopters’ did. Adopters is the set of merchants who share these same characteristics but have indeed adopted subscriptions. I multiplied this average daily by 365 to yield annual effect.
  - ~Important note~: this assumption has both conservative and aggressive components:
    - Conservative: the average daily is computed as the total subscription volume in the dataset / minimum of the ‘days since first charge’ and the total number of days in the dataset. This is conservative, because days since first charge will always be as large or large than ‘days since first subscription charge’. This means our denominator is inflated.
    - Aggressive: we’re assuming that adopters will achieve 100% of this daily average from the very first day, and that it will sustain throughout the following year.
- Cannibalization: 70% of this subscription revenue would be net new (30% cannibazliation factor assumption)

Based on these assumptions, I computed the following ROI estimates:![](Stripe%20Takehome%20Writeup/CleanShot%202024-09-26%20at%2010.39.07.png)
## Conclusion
Targeting 1,300 merchants between the industries, countries, and tenures that were identified through the analysis has the potential to yield incremental subscription volume between $2.4 and $24M in the first year. This represents somewhere between $0.07M and $0.7M in incremental revenue to Stripe in one year. 
## Next Steps

## Next Steps Priority Next Steps: 
1. Refine ROI calculations using model coefficients for more accurate conversion rate estimates 
2. Analyze recent activity data to prioritize merchants within our target list
3. Conduct stakeholder interviews to align our approach with broader strategic goals These steps will significantly enhance the precision and strategic alignment of our recommendations.
### If I Had More Time
- ROI Calculations
  - Calculate expected conversion rate with the regression model using the coefficients, rather than just estimating crude conversion rates
  - Calculate smarter prediction for estimated lift in sales, rather than just using the average daily subscription revenue for previous adopters.
- Filter the target merchant list for merchants who have been active recently.

### If I Had More Data
- Revisit ‘successful adopters of subscriptions’ approach with larger data sets
- Access past learnings from marketing about successful and unsuccessful campaigns.
- Look outside this date range to understand before/after subscription data for subscription adopters
- Spend time understanding the broader context with stakeholders. This approach was based on finding high propensity merchants, but it is conceivable that we would want to take a different approach. For instance, there were markets and industries with low subscription adoption and penetration (for example, large customers in GB). Depending on our strategy, it may make sense to target them with a different sort of campaign, for example a sales heavy one.
## Appendix
### Visualizations of Relationship Between Features and Outcome Variable
![](Stripe%20Takehome%20Writeup/image.png)![](Stripe%20Takehome%20Writeup/image%202.png)