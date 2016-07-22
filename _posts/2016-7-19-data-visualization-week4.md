---
layout: post
title: Data Visualization - Week 4
published: true
---

Now is the time in that we going to begin to visualize our variable with graphs.
Though three or more variable could be selected, in a name of clarity and simplicity, I opted for only 2: Life Expectancy and alcohol consumption. For more information about my project see [here](https://sidon.github.io/data-visualization-week1/)

+ [Univariate histograms for quantitative variables](#univar1)
  + [Univariate for alcohol ](#univar1)
    + [descriptive statistics](#desc1)
  + [Univariate for life](#univar2)
    + [descriptive statistics](#desc2)

+ [Scatterplot ](#scatter1)

During the second week, I created the Categorical Variables and the respective Data dictionary ([See here](https://sidon.github.io/data-visualization-week3/#categorical)), Now   

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
For code, see section [NN] and [NN] on this notebook.

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
For code, see section [NN] and [NN] on this notebook.

### <a name = "scatter1"></a>Scatterplot for the association between Alcohol Consumption and Life Expectancy:
![Scatter1](/images/scatter1.png)

For code, see section [NN] and [NN] on this notebook.

## <a name = "barqt"></a>Univariate bar graphs for categorical variables

### <a name = "unicateg1"></a>Univariate bar graph for categorical variable life:

![Categ1](/images/unicateg_life.png)

For code, see section [NN] and [NN] on this notebook.

### <a name = "unicateg1"></a>univariate bar graph for categorical variable alcohol

![Categ2](/images/unicateg_alcohol.png)

For code, see section [NN] and [NN] on this notebook.


### <a name = "unicateg1"></a>Bivariate bar graph

![Bivar1](/images/bivar.png)

For code, see section [NN] and [NN] on this notebook.
