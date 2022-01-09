# Overview 

The main objective of this project is to analyze customer data to improve promotional strategy and eventually to optimize targeted marketing campaigns by maximizing profits and minimizing advertising cost.

# Dataset

The dataset used in this project was originally used as a take-home assignment provided by Starbucks for their job candidates. The data consists of about 120,000 data points split in a 2:1 ratio among training and test files. In the experiment simulated by the data, an advertising promotion was tested to see if it would bring more customers to purchase a specific product priced at $10. Since it costs the company 0.15 to send out each promotion, it would be best to limit that promotion only to those that are most receptive to the promotion. Each data point includes one column indicating whether or not an individual was sent a promotion for the product, and one column indicating whether or not that individual eventually purchased that product. Each individual also has seven additional features associated with them, which are provided abstractly as V1-V7.

# Optimization Metrics

The promotional strategy will be evaluated on 2 key optimization metrics:

* **Incremental Response Rate (IRR)**: IRR depicts how many more customers purchased the product with the promotion, as compared to if they didn't receive the promotion. Mathematically, it's the ratio of the number of purchasers in the promotion group to the total number of customers in the purchasers group (_treatment_) minus the ratio of the number of purchasers in the non-promotional group to the total number of customers in the non-promotional group (_control_).

* **Net Incremental Revenue (NIR)**: NIR depicts how much is made (or lost) by sending out the promotion. Mathematically, this is 10 times the total number of purchasers that received the promotion minus 0.15 times the number of promotions sent out, minus 10 times the number of purchasers who were not given the promotion.

# Sanity Check: Invariant Metrics

To ensure the experiment was run properly, we first need to make sure that all invariant metrics pass the sanity check. We would expect that these metrics do not differ significantly between control and experiment group. Otherwise, this would imply that someting is wrong with the experiment setup and that our results are biased. We might then have to look at the day by day data and see if we can offer any insight into what is causing the problem.

# Results Analysis: Evaluation Metrics

## Check for Practical and Statistical Significance

Next, for our evaluation metrics, calculate a 95% confidence interval for the difference between the experiment and control groups, and check whether each metric is statistically and/or practically significance.

# Uplift Modeling

 Uplift Modeling is a predictive modelling technique that directly models the incremental impact of a treatment (such as a direct marketing action) on an individual’s behavior. In other words, it can help to identify individuals who will purchase the products only as a result of receiving a discount coupon or a personalized advertisement.

The approach is to see how each variable or combination of variables along with a promotion influences the chance of purchasing. Therefore, we need to identify customers who will make a purchase only after they were given a promotion. We can do this by assigning labels of 1 to individuals that received a promotion and made a purchase, and labels of 0 to everyone else. 

Next, we build a model to select the best customers to target that maximizes the Incremental Response Rate and Net Incremental Revenue.

# Model Evaluation 

There are four possible outcomes of the classification model:

Table of actual promotion vs. predicted promotion customers:  

<table>
<tr><th></th><th colspan = '2'>Actual</th></tr>
<tr><th>Predicted</th><th>Yes</th><th>No</th></tr>
<tr><th>Yes</th><td>I</td><td>II</td></tr>
<tr><th>No</th><td>III</td><td>IV</td></tr>
</table>

The metrics are only being compared for the individuals we predict should obtain the promotion – that is, quadrants I and II.  Since the first set of individuals that receive the promotion (in the training set) receive it randomly, we can expect that quadrants I and II will have approximately equivalent participants. Comparing quadrant I to II then gives an idea of how well the promotion strategy will work in the future. 

## Training Set Evaluation 

Several classification models were built and compared. The model with the highest mean ROC AUC was chosen to be used to improve promotional strategy In another word, the model that performs the best in identifying customers who will make a purchase after getting a promotion.

## Test Set Evaluation 

When having a strategy for who should receive a promotion, we test the strategy against the test dataset used in the final `test_results` function.