# Subscription Adoption Analysis: Targeting Merchants for Subscription Products

## Executive Summary

Key Findings:
1. Identified 165 target merchants for subscription adoption marketing.
2. Successful adopters showed an average 92% increase in total volume after adopting subscriptions.
3. Small businesses (95%) and specific industries (Business Services, Personal Services, Education, Merchandise) are overrepresented among successful adopters.
4. Target merchants are primarily from US, GB, AU, and HK, with an average daily volume of $80.45.
5. Only 7 out of 165 target merchants currently use product links, indicating potential for cross-selling.

Recommendations:
1. Focus marketing efforts on the identified 165 target merchants.
2. Tailor messaging to highlight the observed 92% average volume increase among successful adopters.
3. Investigate the low representation of medium and large businesses among successful adopters.
4. Consider bundling subscription offerings with other products like payment links.

Proposed Success Metrics:
1. Subscription Adoption Rate
2. Subscription Volume Growth
3. Subscription Retention Rate

## 1. Data Preparation

The analysis began with importing two datasets: merchants and payments. Initial data exploration revealed several key insights:

1. The payments table contained 1.6M rows of daily merchant payment volume.
2. Most rows had zero values for at least one of the three volume types (subscription, checkout, payment link).
3. Merchant distribution was relatively even across industries but concentrated in certain countries (50% in US and GB).
4. Over 90% of merchants were classified as 'small'.

Data cleaning steps included:
- Converting date columns to datetime format
- Casting merchant and industry columns to string type
- Converting volume columns from cents to dollars
- Removing duplicate merchants with ID '0'

A merged dataset was created, joining merchant and payment data, which formed the basis for subsequent analysis.

## 2. Approach and Rationale

The chosen methodology focused on identifying successful subscription adopters and finding similar merchants to target. This approach was selected because it leverages actual performance data to inform targeting decisions.

Key steps in the analysis:
1. Segmentation Analysis: Examined subscription adoption and penetration across business size, country, and industry.
2. Identifying Successful Adopters: Defined criteria for successful adoption, including growth in average daily volume and minimum activity thresholds.
3. Characterizing Successful Adopters: Analyzed the traits of successful adopters in terms of industry, country, business size, and product usage.
4. Targeting Similar Merchants: Developed criteria to identify merchants similar to successful adopters but not yet using subscriptions.

This approach allows for data-driven targeting based on observed success patterns within the existing merchant base.

## 3. Results

The analysis identified 165 target merchants for subscription adoption marketing. Key characteristics of these targets include:

- Countries: Primarily in US (122), GB (25), AU (12), and HK (6)
- Industries: Business services (51), Software (41), Merchandise (35), Education (24), Personal services (14)
- Product Usage: Only 7 use product links, while 158 do not
- Activity: Average of 11.38 active days in the last 15 days
- Volume: Mean daily volume of $80.45, with a median of $24.38

These merchants represent a group similar to successful adopters but not yet using subscription products.

## 4. Next Steps

Given more resources, the following steps would enhance the analysis:

1. Conduct a more granular time-series analysis to understand adoption patterns and seasonality effects.
2. Develop a predictive model for subscription success, incorporating more features like merchant age, growth trajectory, and customer base characteristics.
3. Perform A/B testing on marketing messages and channels to optimize outreach to target merchants.
4. Analyze customer behavior data to understand which types of end-customers are most likely to engage with subscription offerings.
5. Investigate the reasons for the low representation of medium and large businesses among successful adopters and adjust targeting strategies accordingly.
6. Conduct qualitative research (e.g., interviews) with successful adopters to gain deeper insights into their subscription implementation process and challenges.

## 5. Metrics Proposal

To track the success of encouraging Stripe merchants to adopt subscription products, I propose the following metrics:

1. Subscription Adoption Rate: 
   Definition: Percentage of target merchants who start using subscription products within a specific timeframe (e.g., 3 months) after being targeted.
   Importance: Directly measures the effectiveness of the targeting and outreach efforts.

2. Subscription Volume Growth:
   Definition: Percentage increase in total subscription volume for newly-adopted merchants over their first 6 months of usage.
   Importance: Indicates the impact of subscription adoption on merchant's overall volume and, by extension, Stripe's revenue.

3. Subscription Retention Rate:
   Definition: Percentage of merchants who continue using subscription products 12 months after adoption.
   Importance: Measures the long-term success and satisfaction of merchants with subscription products, indicating sustainable growth.

These metrics provide a comprehensive view of both initial adoption success and long-term impact, allowing for ongoing optimization of targeting and support strategies.

## 6. Lessons Learned

Throughout this analysis, several important lessons emerged:

1. Limited Impact: The final sample size of 165 target merchants is relatively small, which may limit the overall impact of the targeting strategy. Given more time, exploring alternative approaches to identify a larger pool of potential adopters could yield higher ROI.
2. Data Constraints: The analysis was constrained by the available data. More granular data on merchant characteristics and customer behavior could have provided deeper insights and potentially more accurate targeting.
3. Time vs. Depth Trade-off: The time constraint forced a focus on a specific approach, potentially overlooking other valuable strategies. In future analyses, allocating more time for exploratory data analysis and testing multiple approaches could yield more robust results.
4. Overrepresentation of Small Businesses: The overwhelming representation of small businesses (95%) among successful adopters was unexpected and warrants further investigation. This could indicate either a real trend or a bias in the data or analysis method.
5. Limited Product Usage Insights: The lack of clear patterns in product usage (e.g., payment links) among successful adopters was somewhat frustrating and limited our ability to make strong recommendations about cross-selling opportunities.
6. Adoption Timeline Challenges: The criteria for successful adoption, particularly the requirement for 15 days of data before and after adoption, significantly reduced our sample size. This highlights the need for longer-term data to truly understand adoption patterns.
7. Potential for Broader Strategies: While the focus on mimicking successful adopters is logical, it may have limited our view of potential opportunities. A broader, more exploratory approach might uncover unexpected patterns or merchant segments ripe for subscription adoption.
8. Volume Unit Oversight: A critical mistake was made in the initial stages by not realizing that volumes were in cents rather than dollars. This oversight was discovered late in the analysis, leading to less exciting results and insufficient time to redo the work. This emphasizes the importance of thoroughly understanding the data units from the outset.
9. Alternative Approach Consideration: Given the challenges faced, a propensity modeling approach (finding merchants more likely to adopt subscriptions) might have been more fruitful. This approach could have potentially yielded a larger and more diverse set of target merchants.
10. Stakeholder Alignment: The recommendations and approach could vary significantly based on the ideal outcome desired by the head of product and/or marketing. For instance, a sales-focused approach might prioritize a smaller number of larger customers, while a marketing-focused approach might align more with the broader targeting strategy we employed.
11. Comparative Growth Analysis: An important step that was overlooked was comparing the growth rates of subscription adopters to the overall dataset. Without this comparison, it's unclear whether the observed growth rates among adopters are truly significant or simply in line with general trends.
12. Balancing Adoption and Success: The attempt to not only find potential adopters but also those likely to be successful post-adoption proved to be a challenging goal. While ambitious, this approach may have overly constrained our results. A two-step process of first identifying potential adopters and then assessing their likelihood of success might be more effective.

These lessons provide valuable insights for future analyses and highlight areas where additional research or data collection could significantly enhance our understanding of subscription adoption patterns and opportunities. They also underscore the importance of early data validation, stakeholder alignment, and considering multiple analytical approaches when tackling complex business questions.