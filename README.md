> [!NOTE]
> If you encounter an error with the Jupyter Notebook on GitHub, please use the following links:
> <br>- [nbviewer: RFM with Polars](https://nbviewer.org/github/Agungvpzz/RFM-Analysis-with-Polars/blob/main/RFM%20with%20Polars.ipynb)
> <br>- [nbviewer: RFM SuperStore](https://nbviewer.org/github/Agungvpzz/RFM-Analysis-with-Polars/blob/main/RFM%20SuperStore.ipynb)

# RFM Analysis
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

## Data Collection
The dataset can be accessed at the following link:
https://www.kaggle.com/datasets/rohitsahoo/sales-forecasting

**RFM Metrics**
- **Recency**: This refers to the number of days since a customer last made a purchase. A higher number indicates a longer gap between purchases, which is generally undesirable for a business.
- **Frequency**: This measures the total number of purchases made by a customer. A higher frequency suggests that the customer is more engaged, which is beneficial.
- **Monetary**: This represents the total amount of money a customer has spent with the business. A higher monetary value is a positive indicator, as it means the customer is contributing more revenue.


## RFM Scoring
<p align="justify">
  In RFM scoring, we categorize our Recency, Frequency, and Monetary metrics into five discrete numerical values, ranging from 1 to 5. Here's how we assign these values:
</p>

- **Recency (R)**: We allocate scores by dividing the values into quantiles, where a lower number of days (i.e., more recent purchases) receives a higher score.
- **Frequency (F)**: Instead of quantiles, we manually categorize these into five groups, with more frequent purchases resulting in a higher score.
- **Monetary (M)**: Similar to Recency, we use quantiles to assign scores, with higher spending resulting in a higher score.

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
- **Hibernating (R1‑2, FM1‑2)**: Customers who have been inactive for an extended period, with a notably low recent engagement and infrequent purchasing behavior.
- **At-Risk (R1‑2, FM3‑4)**: Customers with outdated activity but moderate purchase frequency and spending, suggesting waning interest.
- **Cannot Lose Them (R1‑2, FM5)**: Valuable customers who, despite a long gap since their last purchase, consistently buy frequently and spend high amounts.
- **About to Sleep (R3, FM1‑2)**: Customers with moderate recency but low purchase frequency, indicating they might soon become inactive.
- **Need Attention (R3, FM3)**: Customers showing average behavior across all metrics, requiring focused engagement to keep them active.
- **Loyal Customers (R3‑4, FM4‑5)**: Regular buyers with strong spending habits reflected by decent recent activity and high frequency.
- **Promising (R4, FM1)**: New customers who are recent but have yet to purchase frequently, showing potential for growth.
- **New Customers (R5, FM1)**: Recently acquired customers with few repeat purchases.
- **Potential Loyalists (R4‑5, FM2‑3)**: Customers with promising engagement levels, poised to demonstrate increased loyalty over time.
- **Champions (R5, FM4‑5)**: The top-tier group—highly active, frequent buyers with significant spending.

## Analysis of Results
<div align="center">
  
  ![image](https://github.com/user-attachments/assets/674ac96e-875b-4f16-9ffe-53423ab8b3e4)
</div>

- **Champions** (10.84% of Customers)
  - Percentage of Total Sales: 16.6%
  - Percentage of Total Purchases: 15.32%
- **Loyal Customers** (18.79% of Customers)
  - Percentage of Total Sales: 31.7%
  - Percentage of Total Purchases: 25.29%
- **At-Risk** (13.49% of Customers)
  - Percentage of Total Sales: 18.85%
  - Percentage of Total Purchases: 15.3%
- **Cannot Lose Them** (1.89 % of Customers)
  - Percentage of Total Sales: 4.97%
  - Percentage of Total Purchases: 3.09%
- **Potential Loyalists** (16.14% of Customers)
  - Percentage of Total Sales: 10.52%
  - Percentage of Total Purchases: 14.59%
- **Hibernating** (24.46% of Customers)
  - Percentage of Total Sales: 9.91%
  - Percentage of Total Purchases: 15.77%
- **Need Attention** (3.15% of Customers)
  - Percentage of Total Sales: 3.41%
  - Percentage of Total Purchases: 3.19%
- **About to Sleep** (8.07% of Customers)
  - Percentage of Total Sales: 3.54%
  - Percentage of Total Purchases: 5.83%
- **Promising** (1.26% of Customers)
  - Percentage of Total Sales: 0.16%
  - Percentage of Total Purchases: 0.69%
- **New Customers** (1.89% of Customers)
  - Percentage of Total Sales: 0.34%
  - Percentage of Total Purchases: 0.93%

## Key Findings:
- **Loyal Customer Sales Contribution:**
  - 31.7% of total sales come from Loyal Customers.
  - However, despite their significant contribution, the average recency for this segment exceeds 57.31 days, suggesting that while they purchase frequently enough to be valuable, there is room to improve their purchase frequency or re-engagement.
- **High-Value Segment Dominance:**
  - Champions (10.8% of customers) and Loyal Customers (18.79%) are critical segments, together accounting for 48.3% of total sales and 40.61% of total purchases.
  - This highlights their critical role in driving the business’s revenue, underscoring the need for targeted strategies to nurture and retain these key segments.
- **Inactivity Warning Signs:**
  - A concerning 41.36% of customers have a recency exceeding 100 days, and these inactive customers are responsible for 35.25% of the total sales.
  - Additionally, only 24.46% of customers have engaged within the last 30 days, indicating a significant segment that could benefit from reactivation strategies to boost overall engagement and revenue.

## Conclusions & Recommendations:
- **Loyal Customers and Champions as Revenue Drivers**: Nearly half of total sales and purchases come from these segments. Action: Prioritize personalized engagement to maintain and boost their value.
- **Increase Purchase Frequency**: Loyal Customers are active buyers, yet an average recency of 57.31 days suggests room for more frequent interactions. Action: Deploy targeted promotions to encourage more regular purchases.
- **Reactivate Inactive Customers**: Although 41.36% of customers haven't engaged in over 100 days, they still account for 35.25% of sales. Action: Launch reactivation campaigns to recapture this dormant segment.
- **Enhance Overall Engagement**: With only 24.46% of customers active within the last 30 days, there is significant potential to boost overall activity. Action: Implement broad engagement strategies to stimulate recurring interactions.
