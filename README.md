## Analyze A/B Test Results


## Table of Contents
- [Getting Started](#getting-started)
- [Introduction](#intro)
- [Part I - Probability](#probability)
- [Part II - A/B Test](#ab_test)
- [Part III - Regression](#regression)
- [Conclusions](#conclusions)

<a id='getting-started'></a>
## Getting Started

This project requires Python and the following Python libraries installed:

- [numpy](http://www.numpy.org/)
- [pandas](http://pandas.pydata.org/)
- [matplotlib](http://matplotlib.org/)
- [statsmodels](https://www.statsmodels.org/)

You will also need to have software installed to run and execute a [Jupyter Notebook](https://jupyter.org/).

If you do not have Python installed yet, install the [Anaconda](https://www.anaconda.com/download/#macos) distribution of Python, which already has the above packages and more included.

### Run
In a terminal or command window, run the following command:

    jupyter notebook
    
This will open the Jupyter Notebook software in your browser and you can navigate to the directory where the file is.

<a id='intro'></a>
### Introduction

For this project, I will be analyzing the results of an A/B test run by an e-commerce website.  The goal is to understand if the company should implement the new page, keep the old page, or perhaps run the experiment longer to make their decision.

<a id='probability'></a>
### Part I - Probability

Given that the size of each group is about 50-50 control-treatment, the groups are fairly represented. The conversion rate for the control group is 12.04% while the rate for the treatment group is 11.88%. Even though the control group appears to have a higher conversion rate, the difference is not practically significant and therefore does not indicate to me that one leads to more conversions over the other.

<a id='ab_test'></a>
### Part II - A/B Test 


Under the null and alternative hypotheses below, we assume that the old page is better unless the new page proves to be definitely better at a Type I error rate of 5%. **$p_{old}$** and **$p_{new}$** are the converted rates for the old and new pages.

**H<sub>0</sub>** : **P<sub>new</sub>** - **P<sub>old</sub>** ≤ 0

**H<sub>1</sub>** : **P<sub>new</sub>** - **P<sub>old</sub>** > 0

Assuming under the null hypothesis, P<sub>new</sub> and P<sub>old</sub> both have "true" success rates equal to the **converted** success rate regardless of page - that is **P<sub>new</sub>** and **P<sub>old</sub>** are equal. We also assume they are equal to the **converted** rate in **ab_data.csv** regardless of the page. <br><br>

The p value tells us the proportion of values in the null distribution that are greater than the observed difference. The p value tells us whether we can reject or fail to reject the null hypothesis. The analysis resulted in a p value of 0.85 (very high) which tells us that it is likely our value came from the null hypothesis, meaning we cannot reject it. This means that it likely that there is no difference between the new and old landing pages.

Alternatively, using the built-in statsmodels, the z score of 1.31 and p value of 0.095 confirm the findings from the previous section: that it is likely that our statistic came from the null, therefore we cannot reject the null hypothesis, and it is likely there is no significant difference between the new and old landing pages.

<a id='regression'></a>
### Part III - A regression approach

In this final part, we will see that the result acheived in the previous A/B test can also be acheived by performing regression.<br><br>

The p value associated with ab_page is 0.19, which is different than the 0.85 p value we calculated in Part II, however it is still large enough that we cannot reject the null hypothesis, meaning it is likely there is no difference in the new page versus the old page. The difference in p values is due to the difference in the type of hypothesis. The regression table shows a two-sided confidence interval while the p value from part II was a one-sided test.

Furthermore, there are many other factors that could influence whether an individual converts such as Change Aversion (existing users may give an unfair advantage to the old version simply becasue they don't like change) and Novelty Effect (existing users may give an unfair advantage to the new version because they are excited for the change). Both of the effects do not determine that one is better than the other; they are simply biases that can affect the accuracy of the model. This is why it is important to consider other factors.

<a id='conclusions'></a>


### Conclusions

> This project entails analyzing A/B Testing using various methods to reach the same conclusion. The process starts by looking at simple conversion rates which shows that although there is a slightly higher conversion rate from the new page of 12.04% versus 11.88% from the old page, I do not believe this difference was practically significant.

> The process continues by using hypothesis testing to analyze the null and alternative hypotheses using the bootstrapping technique. This method concludes that the conversions from the new and old landing pages are not significant enough to show a material difference.

> Additionally, we identify that there could be external factors contributing to these results such as the Change Aversion and Novelty Effect biases. 

> Finally, we conclude the project by looking at logistic regression, which also shows that the results were not significant enough to determine a difference in conversions for the old and new page.
