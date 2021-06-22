## Northwind Traders Discount Program Review

**Northwind Traders** has asked us to review their discount program, to determine the effectiveness of the program, and with regard to whether it was being applied equally throughout their organization.  This repository includes our technical review, a high-level overview (with slides), and the database and schema from Northwind utilized to perform the review. 

### Contents of the repository: 
* Index.ipynb: jupyter notebook containing our technical review.
* Readme.md: this file describing the repository.
* JLN Mod3v2 Final.key:  high-level slides (.key)
* JLN Mod3v2 Final.pdf:  high-level slides (.pdf)
* Northwind_ERD_updated.png: database schema
* Northwind_small.sqlite: database

### Questions Addressed:

#### Question 1: Did the discount amount have a statistically significant effect on the quantity of a product in an order? If so, at what level(s) of discount?

<img src="https://github.com/jnels13/Northwind_Traders_Hypothesis_Testing/blob/master/Q_ordered_discounted_v_nondiscounted.png">

For this question, we initially looked at whether a discount had a statistically significant effect on the quantity of a product in an order. The samples are skewed to the right and variances are not similar (306.28 vs. 428.83 -- they're more than 33% apart). Because the sample sizes are large (838 and 1317), Welch's T-test would the appropriate test. After running the test, the returned p-value was 5.02562436e-11. Because the p-value was below .05, we rejected the null hypothesis that there's no difference between the sample mean (meaning there was no statistically significant effect of a discount on the quantity ordered). 

The question next became, **at what level of discount is there a statistically significant effect on quantity ordered (if any)? **

As a starting point, I wanted to review and compare the different quantities ordered at different discount levels:

<img src="https://github.com/jnels13/Northwind_Traders_Hypothesis_Testing/blob/master/Q_ordered_at_different_discount_levels.png">

There were some differences, but overall, the differences did not appear significant across the different discount levels in the box plots. Most significantly, the means were very consistent across the different discount levels. 

However, the ANOVA test returned a p-value of 2.991487e-09; because this is below 0.05, allowing us to reject the null hypothesis (that there's no statistically significant difference between the various samples). The Tukey HSD test showed that we could reject the null hypotheses as to the 5, 15, 20, and 25% discount levels, and that we could conclude that discounts offered a statisticaly significant effect on quantity at the 5, 15, 20, and 25% levels. The 10% discount level had a similar sample size as the first noted set, so we were curious why we couldn't reject the 10% level.

Overall, of those discount levels with a statistically signficant effect, all levels of discounts had the relatively same effect size on quantities ordered. The "effect size" determination only shows the relative effect.

#### Question 2: Do orders that include discounts generate more revenue than those without?

This question examined whether orders with discounts generate more revenue than those without, on the general assumption that people will buy more of a product when it's cheaper. The two samples had 380 and 450 observations, respectively, with somewhat similar variances of 3.58e+06 and 3.21e+06. The distributions were strongly skewed to the right, but the sample sizes were large enough that a Welch's T-test would be an appropriate hypothesis test for these samples.  

Average Revenue Per Order WITH Discounts was $1702.35 and without discounts was $1375.33.  This difference was statistically significant because the returned p-value was 0.01125, which was below the alpha, which allowed us to REJECT the null hypothesis (there was a significant relationship between discounts and quantity ordered). Because the p-value was so low, we could reject the null hypotheses and concluded that there was a statistically significant relationship between the application of discounts and the average revenue per order.

#### Question 3: Do customers who order discounted items have a statistically significant higher order rate than customers who do not order discounted items?

This question examined whether customers with applied discounts order more than customers who do not have discounts applied.  The Average number of orders for customers who had discounts applied was 12.09 orders. The average numer of orders for customers who did NOT have discounts applied was 5.06 orders. This difference was statistically significant because the P-value is 8.04334377e-12, which was below the alpha, allowing us to REJECT the null hypothesis and conclude that there was a significant relationship between discounts applied and the number of orders per customer. Because the p-value was so low, we rejected the null hypothesis and concluded that there was a statistically significant relationship between the application of discounts and the number of orders per customer.  It should be noted that this result was merely corralative; it does not mean that discounts cause additional orders; additional work would be needed to determine this.

#### Question 4: Is there a statistically significant relationship between the employee and how often discounts are applied to orders?  (Do all Northwind employees apply discounts equally to their orders?)

Given the statistically significant relationship between the application of discounts and revenue, we looked at whether the various employees are applying discounts to their orders with the same frequency.

<img src = "https://github.com/jnels13/Northwind_Traders_Hypothesis_Testing/blob/master/Orders_w_Discounts_Applied_Per_Employee.png">

Of the 830 orders, 316 had discounts applied (38%). There are nine employees with orders; we would expect 38% of each employees' orders to have discounts applied (given relationship, above, between discounts and revenue).  Because the data here was exclusively categorical, the appropriate hypothesis test statistic was chi-squared. Inputs for the chi-squared test are the expected and actual observations or each of the nine employees (ID Nos. 1-9).

Because the p-value exceeded our alpha of 0.05, we failed to reject the null hypothesis that there is no significant relationship between employees and the application of discounts per order. In other words, the variance visualized above is likely due to chance, though anecdotally -- as shown above -- employees 2, 3, and 4 are applying fewer discounts per order than the others.

