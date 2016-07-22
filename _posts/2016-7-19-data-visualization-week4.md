---
layout: post
title: Data Visualization - Week 4
published: true
---

Now is the time in that we going to begin to visualize our variables with graphs.
Though three or more variable could be selected, in the name of clarity and simplicity and for to focus on the hypothesis of the project , I opted for only 2: Life Expectancy and alcohol consumption. For more information about my project, click [here](https://sidon.github.io/data-visualization-week1/).
The entire code for this week can see [here](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/submitw4.ipynb).

+ [Univariate histograms for quantitative variables](#univar1)
  + [Univariate for alcohol ](#univar1)
    + [descriptive statistics](#desc1)
  + [Univariate for life](#univar2)
    + [descriptive statistics](#desc2)

The explanatory and response variables, life expectancy and alcohol consumption respectively, arequantitative, thus are presented in a scatter graph.

+ [Scatterplot ](#scatter1)

During the second week, I created the Categorical Variables and the respective Data dictionary ([See here](https://sidon.github.io/data-visualization-week3/#categorical)), Now the respectives bar graph is showing:

+ [Univariate bar graphs for categorical variables](#barqt)
  + [Bar graph for life](#categ_life)
  + [Bar graph for alcohol](#categ_alcohol)

As the scatter graph had been a bit confused, I decided to convert one of the variable (the dependent) in categorical and then to plot the explanatory/response variable in a bar graph.

+ [Bivariete Bar Graph](#bivar)

Though this not a scientific work, I wrote a conclusion.

+ [Conclusion](#conclusion)

## <a name = "histqt"></a>Univariate histograms for quantitative variables

### <a name = "univar1"></a>Univariate histogram for alcohol consumption:

![Alcohol1](/images/unialcohol1.png)

#### <a name = "desc1"></a>Standard deviation and other descriptive statistics for quantitative variable alcohol

```python
╒═════════╤═════════╤═════════╤═══════╤═══════╤═══════╤═══════╤═══════╕
│   count │    mean │     std │   min │   25% │   50% │   75% │   max │
╞═════════╪═════════╪═════════╪═══════╪═══════╪═══════╪═══════╪═══════╡
│     171 │ 6.78409 │ 4.95145 │  0.05 │ 2.725 │  5.92 │  9.99 │ 23.01 │
╘═════════╧═════════╧═════════╧═══════╧═══════╧═══════╧═══════╧═══════╛
```
For code, see section [66] and [67] on [this jupyter notebook.](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/submitw4.ipynb).

### <a name = "univar2"></a>Univariate histogram for life expectancy:
![Life1](/images/unilife1.png)

#### <a name = "desc2"></a>Standard deviation and other descriptive statistics for quantitative variable life.

```python
╒═════════╤═════════╤═════════╤════════╤════════╤════════╤════════╤════════╕
│   count │    mean │     std │    min │    25% │    50% │    75% │    max │
╞═════════╪═════════╪═════════╪════════╪════════╪════════╪════════╪════════╡
│     171 │ 69.3857 │ 9.72824 │ 47.794 │ 62.747 │ 72.974 │ 76.099 │ 83.394 │
╘═════════╧═════════╧═════════╧════════╧════════╧════════╧════════╧════════╛
```
For code, see section [68] and [69] on [this jupyter notebook](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/submitw4.ipynb).

### <a name = "scatter1"></a>Scatterplot for the association between Alcohol Consumption and Life Expectancy:
![Scatter1](/images/scatter1.png)

For code, see section [70] on [this jupyter notebook](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/submitw4.ipynb).

## <a name = "barqt"></a>Univariate bar graphs for categorical variables

### <a name = "categ_life"></a>Univariate bar graph for categorical variable life:

![Categ1](/images/unicateg_life.png)

For code, see section [71] on [this jupyter notebook](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/submitw4.ipynb).

### <a name = "categ_alcohol"></a>univariate bar graph for categorical variable alcohol

![Categ2](/images/unicateg_alcohol.png)

For code, see section [72] on [this jupyter notebook](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/submitw4.ipynb).


### <a name = "bivar"></a>Bivariate bar graph

![Bivar1](/images/bivar.png)

For code, see section [74] and [this jupyter notebook](https://github.com/Sidon/Sidon.github.io/blob/master/_posts/submitw4.ipynb).

### <a name = "conclusion"></a>Conclusion
Analysing only the scatter graph seems do not be a correlation between the variables, but considering the bivariate bar graph we can say that moderate alcohol consumption can contribute to life expectancy increases.
Of course, this not a scientific work and have value only for this context.
