# Udacity Analyse A/B Test Results

## Project Overview

This is the second Udacity Data Analyst project I worked on where I analysed A/B test results by an E-commerce website. 

The company had developed a new web page in order to try and increase the number of users who "convert," meaning the number of users who decide to pay for the company's product. 

My goal was to work through this notebook to help the company understand if they should implement this new page, keep the old page, or perhaps run the experiment longer to make their decision.

**I used the following libraries to work through the project:**

 - Pandas
 - Numpy
 - Random
 - Matplotlib
 - statsmodels.api
 - statsmodels.stats.proportion import proportions_ztest
 - scipy import stats
 
## The project was split into 3 parts as follows:

### Part 1 - Probability

I used the following dataset to analyse the traffic split and conversion rates of the A/B test results:

 - ab_data.csv

**Conclusions:**

 - The test looks like it was run fairly as evidenced by the fact that almost 50% of individuals recieved the new page from analysing the data from the df2 dataframe.

 - The conversion rate was slightly smaller for the treatment group versus the conntrol group. From looking at the evidence we cannot conclude that the trea
 
### Part 2 - A/B Test

I worked off the same dataset (ab_data.csv) as Part 1. For this part I ran a statistical significance test via Bootstrapping in order to understand whether the difference in conversion rates between two pages are significant.

**Conclusions from Bootstrapping:**

Our hypothesis were set to the following:

  Null Hypothesis:  𝑝𝑛𝑒𝑤  =<  𝑝𝑜𝑙𝑑  
  Alternative Hypothesis:  𝑝𝑛𝑒𝑤  >  𝑝𝑜𝑙𝑑 

From looking at the histogram distribution for our simulation. We can see that more than half of the distribution points are greater than the observed statistic. This can be quantified by having obtained the following p-value:

**0.90510000000000002**

Given that the p value is greater than the type 1 error rate threshold of 5%. We do not have statistically signficant results to suggest that the new page is better at converting versus the old page.

Therefore we fail to reject the null hypothesis!

#### Z-score test

I also conducted a z score test using the following library in order to cross check results obtained from bootstrapping:

 - statsmodels.stats.proportion import proportions_ztest

The test outputted the following results:

**p-value = 0.90517370514059103**

**z-score = 1.3116075339133115**

The p value again comes above the type 1 error threshold rate indicating that the observed statistic is not statistically signficant. Which therefore enables us to fail to reject the hypothesis.

The Z score tells us how many standard deviations a data point is from the mean. A larger Z score value indicates that the result was unlikely due to chance.

### Part 3i - Regression

I worked off the same dataset (ab_data.csv) as Part 1 and Part 2. In this part I ran a logistic regression model to analyse the same A/B test results as part 2.

**Conclusions from Logistic Regression model:**

From the regression model, we interpretted the new page to be 1.16x less likely to convert a user holding all other variables constant.

We saw the p value wass 0.190, which is greater than the type 1 error threshold, indicating that that the relationship between the ab_page and the dependent variable (converted) is not statistically significant.

For the regression model the null and alternative hypothesis is as follows:

Null Hypothesis:  𝑝𝑛𝑒𝑤  =  𝑝𝑜𝑙𝑑 

Alternative Hypothesis:  𝑝𝑛𝑒𝑤  !=  𝑝𝑜𝑙𝑑 

This is different from the part 2 section of this report where we were testing whether the new page is better than the old page. Whilst the regression model is testing to see if there is a difference between the new page and old page. S

This is the reason why we see different p values between Part 2 and Part 3 of this report.

### Part 3ii - Regression

In the section section of part 3 I wanted to understand whether the country of origin had an impact on conversion. This required loading the following dataset:

 - countries.csv

**Conclusions from Logistic Regression model against countries:**

 - A user who gets the treatment page from Canada is 1.08x less likely to convert compared to a user who gets the treatment page from the US holding all other variables constant. Whilst we can say this relationship is statistically significant given that the p value is 0.046. We wouldn't say this is practically significant.

 - A user who gets the treatment page from UK is 1.02x more likely to convert compared to a user who gets the treatment page from the US holding all other variables constant. From looking at the p value we can't say that this relationship is statistically significant.
