# RFM Analysis Report
## Introduction
<p align="justify">
  The purpose of this report is to analyze our customer base using the RFM (Recency, Frequency, Monetary) model. 
  RFM analysis is a powerful tool for understanding customer behavior, allowing businesses to segment customers based on how recently they make a purchase, 
  how frequently they make purchases, and how much they spend.
  In this report, we aim to gain insights into our customer demographics, identify high-value customers, 
  and determine the best strategies for improving customer engagement and retention. 
  By applying the RFM model, we can categorize customers into various segments, enabling us to tailor marketing efforts, optimize resource allocation, 
  and improve the customer experience.
</p>

## Data Collection and Preparation
<p align="justify">
  The Online Retail II dataset provides detailed insights into the sales activities of an online store from December 1, 2009, to December 9, 2011. This dataset is available on Kaggle. The company specializes in unique giftware suitable for a variety of occasions. A substantial portion of the customer base consists of wholesalers.
  RFM Metrics
</p>

- **Recency**: This refers to the number of days since a customer last made a purchase. A higher number indicates a longer gap between purchases, which is generally undesirable for a business.
- **Frequency**: This measures the total number of purchases made by a customer. A higher frequency suggests that the customer is more engaged, which is beneficial.
- **Monetary**: This represents the total amount of money a customer has spent with the business. A higher monetary value is a positive indicator, as it means the customer is contributing more revenue.


## RFM Scoring
<p align="justify">
  In RFM scoring, we categorize our Recency, Frequency, and Monetary metrics into five discrete numerical values, ranging from 1 to 5. Here's how we assign these values:
</p>

- Recency (R): We allocate scores by dividing the values into quantiles, where a lower number of days (i.e., more recent purchases) receives a higher score.
- Frequency (F): Instead of quantiles, we manually categorize these into five groups, with more frequent purchases resulting in a higher score.
- Monetary (M): Similar to Recency, we use quantiles to assign scores, with higher spending resulting in a higher score.

<p align="justify">
  After scoring these three metrics, we compute an intermediate score by averaging the Frequency and Monetary scores. 
  We then concatenate this average with the Recency score to form the final RFM score. 
</p>

**Here's an example**: <br>
If Recency (R) is 5, Frequency (F) is 1, and Monetary (M) is 3, the intermediate score is calculated as (1+3)/2=2. <br>
The final RFM score is a concatenation of Recency and this intermediate score, resulting in a score of "52."

## Customer Segmentation
<p align="justify">
  To segment our customers based on their RFM scores, we use a mapping strategy with regular expressions (regex) in pandas. 
  This approach allows us to categorize customers into distinct segments according to their RFM scores. 
</p>  
Here's how we create the mapping and what each segment represents:

```
seg_map = {
    r"[1-2][1-2]": "Hibernating",
    r"[1-2][3-4]": "At-Risk",
    r"[1-2]5": "Cannot Lose Them",
    r"3[1-2]": "About to Sleep",
    r"33": "Need Attention",
    r"[3-4][4-5]": "Loyal Customers",
    r"41": "Promising",
    r"51": "New Customers",
    r"[4-5][2-3]": "Potential Loyalists",
    r"5[4-5]": "Champions",
}
```

With this mapping, we can classify customers into the following segments:
- **Hibernating**: Customers with lower Recency and Frequency scores, indicating they haven't purchased recently and don't buy often.
- **At-Risk**: Customers with low Recency but moderate Frequency and Monetary scores, suggesting they might be losing interest.
- **Cannot Lose Them**: Customers with low Recency but high Frequency and Monetary scores, indicating they are valuable despite their recent inactivity.
- **About to Sleep**: Customers with moderate Recency and low Frequency, suggest they might stop buying soon.
- **Need Attention**: Customers with moderate scores across all metrics, require targeted engagement to prevent them from losing interest.
- **Loyal Customers**: Customers with moderate-to-high Frequency and Monetary scores, indicating they are regular buyers with considerable spending.
- **Promising**: Customers with high Recency but low Frequency, suggesting they are new but have potential for more engagement.
- **New Customers**: Customers with high Recency and low Frequency, indicating they are recent additions but with less activity.
- **Potential Loyalists**: Customers with moderate Recency and higher Frequency and Monetary scores, suggesting they might become more loyal over time.
- **Champions**: Customers with high Recency, Frequency, and Monetary scores, representing the best and most active customers.

## Analysis of Results
- Champions (14.2% of Customers)
  - Percentage of Total Sales: 52.8%
  - Percentage of Total Purchases: 43.6%
- Loyal Customers (20% of Customers)
  - Percentage of Total Sales: 29%
  - Percentage of Total Purchases: 30%
- At-Risk (14% of Customers)
  - Percentage of Total Sales: 6.8%
  - Percentage of Total Purchases: 8.3%
- Cannot Lose Them (1.3 % of Customers)
  - Percentage of Total Sales: 3,7%
  - Percentage of Total Purchases: 3%
- Potential Loyalists (12.7% of Customers)
  - Percentage of Total Sales: 2.9%
  - Percentage of Total Purchases: 5.5%
- Hibernating (24.6% of Customers)
  - Percentage of Total Sales: 2.4%
  - Percentage of Total Purchases: 4.9%
- Need Attention (5.2% of Customers)
  - Percentage of Total Sales: 1.5%
  - Percentage of Total Purchases: 2.6%
- About to Sleep (5.7% of Customers)
  - Percentage of Total Sales: 0.6%
  - Percentage of Total Purchases: 1.2%
- Promising (1.6% of Customers)
  - Percentage of Total Sales: 0.1%
  - Percentage of Total Purchases: 0.3%
- New Customers (0.7% of Customers)
  - Percentage of Total Sales: 0.04%
  - Percentage of Total Purchases: 0.1%

## Pareto Principle Applied to RFM Analysis
<p align="justify">
  The RFM analysis indicates that Champions (14.2% of customers) and Loyal Customers (20%) are critical segments, 
  together accounting for 81.8% of total sales and 73.6% of total purchases. This aligns with the Pareto Principle, 
  where a small percentage of customers drive the majority of the sales. 
  Therefore, prioritizing retention and engagement strategies for these top segments is essential. 
  Efforts should also be directed at re-engaging At-Risk (14%) and Cannot Lose Them (1.3%) segments to prevent potential loss, 
  while nurturing Potential Loyalists (12.7%) to further boost their contributions. 
  Focusing on these key customer groups will optimize resources and significantly enhance overall sales performance.
</p>

## Overall Recommendations
- **Focus on High-Value Segments**: Prioritize retention and engagement efforts for Champions and Loyal Customers as they drive the majority of sales and purchases.
- **Re-engagement Strategies**: Implement targeted campaigns for At-Risk, Cannot Lose Them, and Hibernating customers to prevent churn and reactivate their purchasing behavior.
- **Nurture Potential**: Develop strategies to encourage Potential Loyalists and Promising customers to increase their engagement and spending.
- **Onboarding New Customers**: Invest in effective onboarding and nurturing programs to convert New Customers into repeat buyers.

## Conclusion
<p align="justify">
  The RFM analysis reveals that Champions (14.2% of customers) are the most valuable, contributing 52.8% of total sales and 43.6% of purchases, and should be prioritized for retention. 
  Loyal Customers (20%) also significantly contribute, making up 29% of sales and 30% of purchases. 
  At-risk and Cannot Lose Them segments, though smaller, require immediate re-engagement to prevent churn. 
  Potential Loyalists and Hibernating customers present opportunities for growth with targeted marketing. 
  The rest of the segments, including New Customers, need strategic nurturing to boost their engagement and value. 
  Focusing efforts on these key segments can enhance overall customer retention and sales.
</p>


