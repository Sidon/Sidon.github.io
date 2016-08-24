---
layout: post
title: Data Analysis Tools - Week4 | Exploring Statistical Interactions
published: false
---

This is the fourth assignment or the second course (of five) [Data Analysis and Interpretation Specialization](https://www.coursera.org/specializations/data-analysis) detailed information about it can be seeing [here](https://www.coursera.org/learn/data-visualization#).

## Assignment 4:
The fourth assignment deals with testing a potential moderator. When testing a potential moderator, we are asking the question whether there is an association between two constructs for different subgroups within the sample.

See the entire code for this week  [here](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/tools-submitw3.ipynb).

+ [Variables](#variables)
+ [Correlation Coeficient](#correlation)
+ [Scatter Plot](#scatter)
+ [Conclusion](#conclusion)

### <a name = "variables"></a>Variables

Details of my project can seeing [here](https://sidon.github.io/data-visualization-week1/), to get easier, I
made a summary bellow:

|Variable Name|Description|
|-------------|-----------|
|Life         |Explanatory Variable: Life Expectancy (1)|
|Alcohol      |Response Varialbe: Alcohol Consumption (2)|

(1) 2008 alcohol consumption per adult (liters, age 15+)

(2) 2011 life expectancy at birth (years)

### <a name = "correlation"></a>Correlation Coeficient
The association between life expectancy and alcohol consumption is very weak (less than 0.5), thus, the square r show us this weakness.

```python
r1 = scipy.stats.pearsonr(data1['life'], data1['alcohol'])
r1 = list(r1)
r1.insert(2,r1[0]*r1[0])
print (tabulate([r1], tablefmt="fancy_grid",
        headers=['Correlation coefficient', 'P-value', 'r²'] ))
```

|   Correlation coefficient |     P-value |        r² |
|--------------------------:|------------:|----------:|
|                  0.312994 | 2.34203e-05 | 0.0979652 |

The correlation is approximately 0.31 with a very small p-value, this indicates
that the relationship is statistically significant, but the linear correlation
between alcohol consumption and life expectancy is very weak.

The code for this table can seeing in section [2] on [this jupyter notebok](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/tools-submitw3.ipynb)

###  <a name = "scatter"></a> Scatter Plot:

To reinforce the results of the correlation coefficient, I plotted the scatter
plot, that shows us a positive line that demonstrates the dispersion of dots,
indicating the weakness of correlation between the two variables.

```python
scat1 = seaborn.regplot(x="alcohol", y="life", fit_reg=True, data=data1)
plt.xlabel('Alcohol Consumption')
plt.ylabel('Life Expectancy')
plt.title('Scatterplot for the Association Between Life Expectancy and Alcohol Consumption')
plt.show()

```
![Scatter plot](/images/scatter2.png)

The code for this graph can seeing in section [3] on [this jupyter notebok](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/tools-submitw4.ipynb)

### <a name = "conclusion"></a>Conclusion
Although the [correlation calculus](#correlation) shows a p-value<0.05 that
means to reject the null hypothesis (which says there is no correlation) and
accept the alternative hypothesis (which says there is a correlation),
indicating a statistical significance. The r value of 0.312994 shows a very
modest positive linear correlation between alcohol consumption and life expectancy.

See the entire code for this week  [here](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/tools-submitw3.ipynb
  ).
