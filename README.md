## Northwind Traders Discount Program Review

**Northwind Traders** has asked us to review their discount program, to determine the effectiveness of the program, and with regard to whether it is being applied equally throughout their organization.  This repository includes our technical review, a high-level overview (with slides), and the database and schema from Northwind we utilized to perform the review. 

### Contents of the repository: 
* Index.ipynb:  jupyter notebook containing our technical review.
* Readme.md: this file describing the repository.
* JLN Mod3v2 Final.key:  high-level slides (.key)
* JLN Mod3v2 Final.pdf:  high-level slides (.pdf)
* Northwind_ERD_updated.png:  database schema
* Northwind_small.sqlite:  database

### Questions Addressed:

#### Question 1: Does discount amount have a statistically significant effect on the quantity of a product in an order? If so, at what level(s) of discount?

<img src="https://github.com/jnels13/Northwind_Traders_Hypothesis_Testing/blob/master/Q_ordered_discounted_v_nondiscounted.png">

For this question, we initially looked at whether a discount had a statistically significant effect on the quantity of a product in an order. Because the p-value is below .05, we rejected the null hypothesis that there's no difference between the sample mean (meaning there was no statistically significant effect of a discount on the quantity ordered). The question next became, at what level of discount is there a statistically significant effect on quantity ordered (if any)? 

<img src="https://github.com/jnels13/Northwind_Traders_Hypothesis_Testing/blob/master/Q_ordered_at_different_discount_levels.png">

Here, the visualization above shows relatively similar distributions across the different discount levels.  However, the ANOVA test shows a P value < 0.05, allowing us to reject the null hypothesis (that there's no statistically significant difference between the various samples). The Tukey HSD test showed that we can reject the null hypotheses as to the 5, 15, 20, and 25% discount levels, and conclude that Discounts offer a statisticaly significant effect on quantity at the 5, 15, 20, and 25% levels. The 10% discount level has a similar sample size as the first noted set, so we're curious why we couldn't reject the 10% level.

Overall, of those discount levels with a statistically signficant effect, all levels of discounts had the relatively same effect size on quantities ordered. The "effect size" determination only shows the relative effect.

#### Question 2: Do orders that include discounts generate more revenue than those without?

This question will examine whether orders with discounts generate more revenue than those without, on the general assumption that people will buy more of a product when it's cheaper. The two samples have 380 and 450 observations, respectively, with somewhat similar variances of 3.58e+06 and 3.21e+06. The distributions are strongly skewed to the right, but the sample sizes are large enough that a Welch's T-test would be an appropriate hypothesis test for these samples.  

Average Revenue Per Order WITH Discounts is $1702.35 and without discounts is $1375.33.  This difference is statistically significant because the P-value is 0.01125, which is below the alpha, allowing us to REJECT the null hypothesis (there is a significant relationship between discounts and quantity ordered. Because the P-value is so low, we can reject the null hypotheses and conclusde that there is a statistically significant relationship between the application of discounts and the average revenue per order.

#### Question 3: Do customers who order discounted items have a statistically significant higher order rate than customers who do not order discounted items?

This question will examine whether customers with applied discounts order more than customers who do not have discounts applied.  The Average number of orders for customers who have discounts applied is 12.09 orders. The average numer of orders for customers who do NOT have discounts applied is 5.06 orders. This difference is statistically significant because the P-value is 8.04334377e-12, which is below the alpha, allowing us to REJECT the null hypothesis and conclude that there is a significant relationship between discounts applied and the number of orders per customer. Because the P-value is so low, we can reject the null hypothesis and conclude that there is a statistically significant relationship between the application of discounts and the number of orders per customer.  It should be noted that this result is merely corralative; it does not imply that discounts cause additional orders. Additional work would be needed to determine this.

#### Question 4: Is there a statistically significant relationship between the employee and how often discounts are applied to orders?  (Do all Northwind employees apply discounts equally to their orders?)

Given the statistically significant relationship between the application of discounts and revenue, we wanted to look at whether the various employees are applying discounts to their orders with the same frequency.

<img src = "https://github.com/jnels13/Northwind_Traders_Hypothesis_Testing/blob/master/Orders_w_Discounts_Applied_Per_Employee.png">

Of the 830 orders, 316 had discounts applied (38%) had discounts applied. There are nine employees with orders; we would expect 38% of each employees' orders to have discounts applied (given relationship, above, between discounts and revenue).  Because the data here is exclusively categorical, the appropriate hypothesis test statistic is chi-squared. Inputs for the chi-squared test are the expected and actual observations or each of the nine employees (ID Nos. 1-9).

Because the P-value exceeds our alpha of 0.05, we fail to reject the null hypothesis that there is no significant relationship between employees and the application of discounts per order. In other words, the variance visualized above is likely due to chance, though anecdotally (as shown above), employees 2, 3, and 4 are applying fewer discounts per order than the others.

