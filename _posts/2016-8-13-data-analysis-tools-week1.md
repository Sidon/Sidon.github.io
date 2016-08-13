
This is the first assignment or the second course (of five) [Data Analysis and Interpretation Specialization](https://www.coursera.org/specializations/data-analysis) detailed information about it can be seeing [here](https://www.coursera.org/learn/data-visualization#).

## Assignment 1:
On the first course, I have selected a dataset and research question, managed my variables of interest and visualized their relationship graphically. Now is time to test that relationship statistically.
[click here](https://sidon.github.io/data-visualization-week1/)for details for this project

My primary hypothesis was defined:
The level of alcohol consumption of a country might be directly related to expectancy life.

For this assignment is necessary to define null hypothesis (h0) and alternative hypothesis (my primary hypothesis), then h0 is the negation of my primary hypothesis.

My numerical variable is the life expectancy and the categorical is a five levels variable, this is, the alcohol consumption (in liters) divided into 5 ranges:

### <a name = "dictionary"></a>Data Dictionary

| Alcohol    | Description  
|------------|----------------------------------------------
| >=0.5  <5  | Alcohol consumption between 0.5 and 5 litters
| >=5    <10 | Alcohol consumption between 5 and 10 litters
| >=10   <15 | Alcohol consumption between 10 and 15 litters
| >=15   <20 | Alcohol consumption between 15 and 20 litters
| >=20   <25 | Alcohol consumption between 20 and 25 litters

### F-Static
Bellow the code and output or F-statics is showed:

```python
model1 = smf.ols(formula='life ~ C(alcohol)', data=data2)
results1 = model1.fit()
print (results1.summary())

OLS Regression Results                            
==============================================================================
Dep. Variable:                   life   R-squared:                       0.125
Model:                            OLS   Adj. R-squared:                  0.105
Method:                 Least Squares   F-statistic:                     6.112
Date:                Sat, 13 Aug 2016   Prob (F-statistic):           0.000128
Time:                        17:48:59   Log-Likelihood:                -639.68
No. Observations:                 176   AIC:                             1289.
Df Residuals:                     171   BIC:                             1305.
Df Model:                           4                                         
Covariance Type:            nonrobust                                         
==========================================================================================
 coef    std err          t      P>|t|      [95.0% Conf. Int.]
------------------------------------------------------------------------------------------
Intercept                 65.9337      1.060     62.212      0.000        63.842    68.026
C(alcohol)[T.>=5 <10]      3.6651      1.625      2.255      0.025         0.457     6.873
C(alcohol)[T.>=10 <15]     9.5628      1.978      4.834      0.000         5.658    13.468
C(alcohol)[T.>=15 <20]     5.6221      3.126      1.798      0.074        -0.548    11.793
C(alcohol)[T.>=20 <25]     3.3833      9.360      0.361      0.718       -15.093    21.860
==============================================================================
Omnibus:                       16.670   Durbin-Watson:                   1.863
Prob(Omnibus):                  0.000   Jarque-Bera (JB):               19.421
Skew:                          -0.804   Prob(JB):                     6.06e-05
Kurtosis:                       2.746   Cond. No.                         14.4
==============================================================================

Warnings:
[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
```
As the p-value is less than 0.05, it would be safe to reject the null hypothesis if my categorical variable was only 2 levels.

### Post Hoc Test

As my categorical variable has more than two levels, is necessary to apply a post hoc test, for this I used the Tukey's Honestly Significant Difference Test.

```python
mc1 = multi.MultiComparison(data2['life'], data2['alcohol'])
res1 = mc1.tukeyhsd()
print(res1.summary())

Multiple Comparison of Means - Tukey HSD,FWER=0.05
==================================================
 group1   group2  meandiff  lower    upper  reject
--------------------------------------------------
 >=0 <5  >=10 <15  9.5628   4.1087   15.017  True
 >=0 <5  >=15 <20  5.6221  -2.9969  14.2411 False
 >=0 <5  >=20 <25  3.3833  -22.4241 29.1908 False
 >=0 <5  >=5 <10   3.6651  -0.8153   8.1454 False
>=10 <15 >=15 <20 -3.9407  -13.2658  5.3844 False
>=10 <15 >=20 <25 -6.1795  -32.2313 19.8723 False
>=10 <15 >=5 <10  -5.8978   -11.62  -0.1755  True
>=15 <20 >=20 <25 -2.2388  -29.1318 24.6542 False
>=15 <20 >=5 <10  -1.9571  -10.7482  6.834  False
>=20 <25 >=5 <10   0.2817  -25.5837 26.1472 False
--------------------------------------------------
```

Through the analysis of these results it is clear that the F test is insufficient in this case because of the 10 comparisons, only 2 have rejected the hypothesis.
