# Business Experiment: Onboarding & Activation Campaign

## Task 1: Business Problem Statement

### Objective
To determine whether the new onboarding and activation campaign (Treatment) should replace the existing onboarding process (Control) to improve user conversion and engagement.

### Decision Impact
The decision directly impacts the product growth strategy, marketing efficiency, and user experience for all new signups to our digital subscription product.

### Success Metrics (What should improve)
* **Conversion Rate:** Percentage of users who convert to a paid plan.
* **Onboarding Completion Rate:** Percentage of users who successfully complete the onboarding flow.
* **Engagement Score:** Improvement in average internal engagement metrics.

### Guardrail Metrics (What risks must be monitored)
To ensure that improvements in conversion are not achieved at the expense of long-term sustainability, we must monitor:
* **Support Ticket Volume:** An increase in tickets per user indicates a faulty or confusing experience.
* **Refund Rate:** A spike in refund requests suggests that the "converted" users are low-quality or were misled.
* **Revenue Quality:** Ensuring the revenue generated is stable and not derived from high-churn cohorts.

### Evidence Required
A statistically significant increase in the conversion rate and onboarding completion rate, supported by neutral or positive movement in engagement scores, while maintaining or reducing the rate of support tickets and refund requests compared to the Control group.

## Task 2: Define the North Star Metric

### Selected North Star Metric: Conversion Rate to Paid Plan
The conversion rate represents the percentage of users who move from the onboarding process to a paid subscription within 30 days of signup.

### Why this is the North Star Metric
This metric acts as the primary indicator of whether the new onboarding campaign is successfully delivering product value that motivates users to pay. It directly reflects the ultimate business objective: transforming a free or prospective user into a revenue-generating customer.

### Supporting Metrics
* **Onboarding Completion Rate:** Necessary to track the health of the funnel, but completion does not equate to value if users do not pay.
* **Engagement Score:** A leading indicator of user health; it informs us about product "stickiness" but doesn't capture the financial success of the campaign.
* **Guardrails (Support Tickets, Refund Rate):** These metrics are essential for validation, but they monitor *sustainability* rather than *growth*.

### Connection to Business Growth
Increasing the conversion rate directly impacts top-line revenue and improves the Customer Acquisition Cost (CAC) efficiency. By converting a higher proportion of signups, we maximize the value derived from our existing traffic sources without necessarily needing to increase marketing spend.

### Risks of Blind Optimization
If we focus exclusively on the conversion rate, we risk:
* **"Forced" Conversions:** Implementing aggressive sales tactics that may lead to higher initial signups but result in long-term churn.
* **Declining Customer Satisfaction:** A high conversion rate might be achieved by misleading users, leading to an increase in support tickets and refund requests.
* **Cannibalization:** We might convert users who would have purchased anyway, or worse, exhaust a cohort that is not yet ready to pay, damaging brand reputation.

## Task 4: Data Cleaning and Preparation

To ensure the integrity of the experiment analysis, the following data cleaning steps were performed:

1. **Missing Values**: Identified missing values in `days_to_convert`. These were expected as they represent users who have not yet converted to a paid plan. No imputation was performed to avoid biasing conversion metrics.
2. **Group Counts**: Verified balanced distribution between Control and Treatment groups.
3. **Duplicate User IDs**: Checked for duplicate `user_id` entries; none were found, ensuring unique user-level tracking.
4. **Invalid Binary Values**: Validated that all indicator columns (`visited_landing_page`, `started_trial`, etc.) contain only 0 or 1. No invalid values were found.
5. **Outlier Handling Update**: To ensure the analysis focuses on the quality of revenue generated, we refined the outlier detection method. Instead of applying the Interquartile Range (IQR) to the total user base (which is skewed by non-paying users), we restricted the analysis to the **cohort of converting users** (`revenue_30d > 0`).
   - **Q1**: ₹404.02
   - **Q3**: ₹1,178.67
   - **IQR**: ₹774.65
   - **Upper Boundary**: ₹2,340.63
   Any user with a `revenue_30d` exceeding ₹2,340.63 is flagged as an outlier to prevent these values from disproportionately influencing our mean revenue comparisons between groups.
6. **Segment Distribution**: Analyzed the distribution of `region`, `device_type`, and `traffic_source` across `experiment_group` to ensure no selection bias occurred during the randomization process.


# Hypothesis Test Summary

### Primary Metric: Paid Conversion Rate (`converted_to_paid`)
### Statistical Framework: Two-Sample Z-Test for Proportions (Two-Tailed)
### Significance Level ($ lpha$): 0.05 (5%)

#### Calculated Metrics:
* **Z-Statistic**: 3.266 (Critical Boundary: $\pm$1.96)
* **P-Value**: 0.00109

#### Statistical Decision:
**Reject the Null Hypothesis ($H_0$).** Given that our P-value (0.00109) is substantially lower than our alpha threshold (0.05), we confirm that the observed divergence in conversion efficacy is statistically robust and not attributable to random variance.

---

## Guardrail metrics considered
To ensure that immediate conversion improvements do not mask long-term sustainability concerns, we conducted a rigorous assessment of three key operational boundaries:

* **Support Ticket Rate**: Increased notably from 15% (Control) to 25% (Treatment). This signals an elevated operational risk, suggesting that the new onboarding structure may be inducing user friction or confusion.
* **Average Days to Convert**: Decreased from 8.86 days (Control) to 6.40 days (Treatment). This represents a favorable outcome, demonstrating that the new workflow successfully accelerates the user decision-making cycle by 2.46 days.
* **Refund Rate**: Increased from 0.000% (Control) to 0.423% (Treatment). Although this uptick suggests a slight increase in buyer's remorse, it remains well within our defined risk tolerance limit of 1.0%.

---

## Final Recommendation
**Recommendation: Launch Globally with an Immediate Optimization Phase.**

The Treatment experience demonstrates significant commercial potential, effectively more than doubling the paid conversion rate from 3.19% to 7.04% (+3.85% absolute lift) with over 99.9% statistical confidence. 

However, given the concomitant 25% surge in support tickets, the global rollout must be coupled with an immediate, targeted design intervention. Product teams are advised to introduce enhanced on-screen tooltips and provide greater clarity regarding pricing tiers in the upcoming development sprint to mitigate service friction and stabilize the Average Revenue Per Converted User (ARPPU).

---

## Assumptions and limitations

* **Sample Horizon Limitation**: This analysis is confined to a 30-day window. It relies on the assumption that conversion velocity and refund behaviors remain consistent over time, and it does not account for potential long-term subscription churn or customer lifetime value (LTV).
* **Data Discrepancy Assumption**: The raw dataset exhibits a slight variance where total conversions count is 72, despite a platform total of 74. We assume these 2 unallocated entries are attributed to tracking anomalies ("Unknown") and do not materially influence the statistical integrity of the primary cohorts.
* **Homogeneity of Traffic**: The analysis presupposes that external marketing factors, advertising spend allocations, and traffic quality remained stable and uniform throughout the experiment period.

---

## Screenshots included
- `summary_metrics.png`
- `hypothesis_test_output.png`
- `kpi_tree_preview.png`
