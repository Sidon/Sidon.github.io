---
layout: post
title: Regression Modeling in Practice - Week4 | Logistic Regression
published: true
---

This is the fourth assignment or the third course (of five)
[Data Analysis and Interpretation Specialization](https://www.coursera.org/specializations/data-analysis)
detailed information about it can be seeing [here](https://www.coursera.org/learn/data-visualization#).

### Index
+ [Variables](#variables)
+ [Sumary of OLS Results](#summary)
  + [Support for hypothesis](#support)
  + [Odds Ratio](#odds)
+ [Addin income variable](#add1)
  + [ New Summary OLS results](#new)
+ [Evidence of confounding variable](#evidence)
+ [OLS Output](#output)  

### <a name = "variables"></a>Variables

Details of my project can be seeing
[here](https://sidon.github.io/data-visualization-week1/), to get easier, I made a summary bellow:

|Variable Name|Description|
|-------------|-----------|
|Income       |Explanatory Variable: GPD per capita (1)|
|Alcohol      |Explanatory Variable:: Alcohol Consumption (3)|
|Life         |Response Variable: Life Expectancy (2)|

(1) 2010 Gross Domestic Product per capita in constant 2000 US$"

(2) 2011 life expectancy at birth (years)

(3) 2008 alcohol consumption per adult (liters, age 15+)

### <a name = "summary"></a>Sumary of OLS Results
The figure bellow represents part of OLS output of my Regression, for detail of
variables see section [Variables](#variables).
First I selected only 2 variables for the initial analysis, later I added another for analysis of confounder.

![plot](/images/ols_bregressionw4.png)

The regression is significant at a P value of less than 0.0001 (highlighted in red), using parameters estimated,  the linear equation can be generated: Life expectancy is a function of -0.21 plus 1.44 times alcohol, but with the logistic regression is appropriated to use odds ratio.

#### <a name = "support"></a>Support hypothesis
Before we analyse the Odds ratio, we can conclude, through these initial results, that socioeconomic have a direct correlation with the level of alcohol consumption of a country. Then, we can reject the null hypothesis.

#### <a name = "odds"></a>Odds Ratio

```python
params = lreg1.params
conf = lreg1.conf_int()
conf['OR'] = params
conf.columns = ['Lower CI', 'Upper CI', 'OR']

print (np.exp(conf))

           Lower CI  Upper CI       OR
Intercept  0.542615  1.213092 0.811321
alcohol    2.143658  8.249307 4.205198
```

The Odds ratios indicate that there's 95% certainty that two parameters odd ratio fall between 2.14 and 8.25, that is, the alcohol consumption above the mean (6.8 liters per year) represents a life expectancy above the mean (69 years) something anywhere from 2.14 to 8.2 times more likely than those countries that have alcohol consumption levels less than the mean.

### <a name = "add1"></a>Adding Income Variable
Here I added the income levels variabe (see section [Variables](#variables)),
for the secoond analysis (see code for this in section [13] on [this notebok](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/bregession-w3.ipynb)

#### <a name = "new"></a>New Summary OLS results
The figure bellow represent the OLS results after I added the income levels.
![plot](/images/ols_bregressionw4-2.png)

#### <a name = "evidence"></a>Evidence of Confounding
Looking at the news results is possible to note that the inclusion of the new variable (income) change the alcohol p value (highlighted in red), this indicates the evidence of confounding.

### <a name = "output"></a>Output of OLS.
See the entire code and output for this week,  [here](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/bregession-w4.ipynb).
