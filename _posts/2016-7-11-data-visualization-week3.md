---
layout: post
title: Data Visualization - Week 3
published: true
---

Data management is the issue of this third week, data management involves making decisions about data, that will help answer the research questions. The main guides for this are the codebook and frequency distributions.

After watching the videos of this week and examine again, (this time in a detailed way), the codebook and frequency distributions, I found out that I have to make some changes.

+ [Rename Variables](#clarity)
+ [Parsing Numeric Values](#parsing)
+ [Missing Values](#missings)
+ [Dropping Missing Values](#drop_missings)
+ [Frequencies Distribution ](#freq1)
+ [Categorical Variables](#categorical)
+ [Dictionary ](#dictionary)
+ [Categorical Frequencies Distribution ](#freq2)
+ [Full Code](#full_code)

### [Rename Variables](#clarity)
Int the Lines 14-15 I renamed variables for convenience and clarity for coding
````python
14 # Rename columns for clarity                                    
15 data1.columns = ['country','income','alcohol','life']
````
In the line 23 is showed the info about the dataset.
````python
# Show info about dataset
23 data1.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 213 entries, 0 to 212
Data columns (total 4 columns):
country    213 non-null object
income     213 non-null object
alcohol    213 non-null object
life       213 non-null object
dtypes: object(4)
memory usage: 6.7+ KB
````
### [Parsing Numeric Values](#Parsing)
The function [pd.to_numeric](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_numeric.html), convert arguments to a numeric types and the parameter 'errors=coerce' setting invalid parsings (Blanks in this case) as NaN value.
In the lines 26-29 this function is applied to each observation (each line of the variables), and then the information of the dataset are presented again.

````python
26 for dt in ('income','alcohol','life') :
27    data1[dt] = pd.to_numeric(data1[dt], 'errors=coerce')
28    
29 print (data1.info())
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 213 entries, 0 to 212
Data columns (total 4 columns):
country    213 non-null object
income     190 non-null float64
alcohol    187 non-null float64
life       191 non-null float64
dtypes: float64(3), object(1)
memory usage: 6.7+ KB
````
### [Missing Values](#missings)
Lines 32-33 displays information about the data set, once again: While it may seem that there are no "missing data" (no null objects) actually missing values are, in this case, the space values in blank. In lines 10 to 20 XXX presented to the code conversion invalid entries (white) for a numpy NaN value as well as the first ten rows of the result.

````python
32 xdata1 = data1[data1.income.isnull() | data1.life.isnull() | data1.alcohol.isnull() | data1.country.isnull()]
33 print (tabulate(xdata1.head(10), headers=['index','Country','Income','Alcohol','Life']))
index  Country                Income    Alcohol     Life
-------  -------------------  --------  ---------  -------
    0  Afghanistan            nan          0.03   48.673
    3  Andorra              21943.3       10.17  nan
    5  Antigua and Barbuda  11894.5        8.17  nan
    8  Aruba                  nan        nan      75.246
   20  Bermuda              62682.1      nan     nan
   34  Cayman Islands         nan        nan     nan
   43  Cook Islands           nan          3.23  nan
   52  Dominica              6147.78       8.68  nan
   61  Faeroe Islands         nan        nan     nan
   65  French Polynesia       nan        nan      75.133
````

### [Dropping Missing Data](#drop_missing)
Since that the objective of this work is investigating the impact of alcohol consumption on the life expectancy, no make sense to consider entries with missing data, thus in the lines 35-37 these entries are dropped.

````python
36 data1 = data1.dropna(axis=0, how='any')
37 print (data1.info())
<class 'pandas.core.frame.DataFrame'>
Int64Index: 171 entries, 1 to 212
Data columns (total 4 columns):
country    171 non-null object
income     171 non-null float64
alcohol    171 non-null float64
life       171 non-null float64
dtypes: float64(3), object(1)
memory usage: 6.7+ KB
````
### [Frequencies Distributions](#freq1)
In the lines 40-68 the frequencies (absolute and relative) are calculate and showed following, for clarity is presented only 10 first.

````python
40 freq_life_n = data1.life.value_counts(sort=False)
41 freq_income_n = data1.income.value_counts(sort=False)
42 freq_alcohol_n = data1.alcohol.value_counts(sort=False)
43
44 # Relative Frequency distributions
45 freq_life_r = data1.life.value_counts(sort=False, normalize=True)
46 freq_income_r = data1.income.value_counts(sort=False, normalize=True)
47 freq_alcohol_r = data1.alcohol.value_counts(sort=False, normalize=True)
48
49 print ('********************************************************')
50 print ('* Absolute Frequencies original variables (first 5)    *')
51 print ('********************************************************')
52 print ('\nlife variable ('+LIFE+'):')
53 print ( tabulate([freq_life_n.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_life_n.index])) )
54 print ('\nincome variable ('+INCOME+'):')
55 print ( tabulate([freq_income_n.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_income_n.index])) )
56 print ('\nalcohol variable ('+ALCOHOL+'):')
57 print ( tabulate([freq_life_n.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_life_n.index])) )
58
59 print ('\n********************************************************')
60 print ('* Relative Frequencies original variables (first 5)    *')
61 print ('********************************************************')
62
63 print ('\nlife variable ('+LIFE+'):')
64 print ( tabulate([freq_life_r.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_life_n.index])) )
65 print ('\nincome variable ('+INCOME+'):')
66 print ( tabulate([freq_income_r.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_income_n.index])) )
67 print ('\nalcohol variable ('+ALCOHOL+'):')
68 print ( tabulate([freq_life_r.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_life_n.index])) )

********************************************************
* Absolute Frequencies original variables (first 5)    *
********************************************************

life variable (2011 life expectancy at birth (years)):
╒══════════╤══════════╤══════════╤══════════╤══════════╕
│   74.788 │   57.937 │   69.317 │   73.456 │   77.005 │
╞══════════╪══════════╪══════════╪══════════╪══════════╡
│        1 │        1 │        1 │        1 │        1 │
╘══════════╧══════════╧══════════╧══════════╧══════════╛

income variable (2010 Gross Domestic Product per capita in constant 2000 US$):
╒════════════════╤═════════════════╤═════════════════╤═════════════════╤═════════════════╕
│   561.70858483 │   5634.00394802 │   22275.7516608 │   772.933344801 │   1975.55190594 │
╞════════════════╪═════════════════╪═════════════════╪═════════════════╪═════════════════╡
│              1 │               1 │               1 │               1 │               1 │
╘════════════════╧═════════════════╧═════════════════╧═════════════════╧═════════════════╛

alcohol variable (2008 alcohol consumption per adult (liters, age 15+)):
╒══════════╤══════════╤══════════╤══════════╤══════════╕
│   74.788 │   57.937 │   69.317 │   73.456 │   77.005 │
╞══════════╪══════════╪══════════╪══════════╪══════════╡
│        1 │        1 │        1 │        1 │        1 │
╘══════════╧══════════╧══════════╧══════════╧══════════╛

********************************************************
* Relative Frequencies original variables (first 5)    *
********************************************************

life variable (2011 life expectancy at birth (years)):
╒════════════╤════════════╤════════════╤════════════╤════════════╕
│     74.788 │     57.937 │     69.317 │     73.456 │     77.005 │
╞════════════╪════════════╪════════════╪════════════╪════════════╡
│ 0.00584795 │ 0.00584795 │ 0.00584795 │ 0.00584795 │ 0.00584795 │
╘════════════╧════════════╧════════════╧════════════╧════════════╛

income variable (2010 Gross Domestic Product per capita in constant 2000 US$):
╒════════════════╤═════════════════╤═════════════════╤═════════════════╤═════════════════╕
│   561.70858483 │   5634.00394802 │   22275.7516608 │   772.933344801 │   1975.55190594 │
╞════════════════╪═════════════════╪═════════════════╪═════════════════╪═════════════════╡
│     0.00584795 │      0.00584795 │      0.00584795 │      0.00584795 │      0.00584795 │
╘════════════════╧═════════════════╧═════════════════╧═════════════════╧═════════════════╛

alcohol variable (2008 alcohol consumption per adult (liters, age 15+)):
╒════════════╤════════════╤════════════╤════════════╤════════════╕
│     74.788 │     57.937 │     69.317 │     73.456 │     77.005 │
╞════════════╪════════════╪════════════╪════════════╪════════════╡
│ 0.00584795 │ 0.00584795 │ 0.00584795 │ 0.00584795 │ 0.00584795 │
╘════════════╧════════════╧════════════╧════════════╧════════════╛
````
### [Creating Categorical Variables](#categorical)
Now is the time to create the categorical variables, for this, I calculate the min and max values of each variable. The code and result are presented in lines 71-89:

````python
71 min_max = OrderedDict()
72 dict1 = OrderedDict()
73
74 dict1['min'] = data1.life.min()
75 dict1['max'] = data1.life.max()
76 min_max['life'] = dict1
77
78 dict2 = OrderedDict()
79 dict2['min'] = data1.income.min()
80 dict2['max'] = data1.income.max()
81 min_max['income'] = dict2
82
83 dict3 = OrderedDict()
84 dict3['min'] = data1.alcohol.min()
85 dict3['max'] = data1.alcohol.max()
86 min_max['alcohol'] = dict3
87
88 df = pd.DataFrame([min_max['income'],min_max['life'],min_max['alcohol']], index = ['Income','Life','Alcohol'])
89 print (tabulate(df.sort_index(axis=1, ascending=False), headers=['Var','Min','Max']))

Var          Min         Max
-------  -------  ----------
Income   103.776  105147
Life      47.794      83.394
Alcohol    0.03       23.01
````

### [Data Dictionary](#dictionary)
Based on min and max values, I created ranges for each variable (k=1000):
Income        |Life          |Alcohol  
--------------|-------------|-------------
1: >=100  <5k | 1: >=40  <50|1: >=0.5  <5
2: >=5k   <10k| 2: >=50  <60|2: >=5    <10
3: >=10k  <20k| 3: >=60  <70|3: >=10   <15
4: >=20K  <30K| 4: >=70  <80|4: >=15   <20
5: >=30K  <40K| 5: >=80  <90|5: >=20   <25
6: >=40K  <50K| NA          |NA


In the lines 100-101, the first 10 lines of the dataset are showed with new variables.

````python
100 data2['income'] = pd.cut(data1.income,[100,5000,10000,20000,30000,40000,50000], labels=['1','2','3','4','5','6        '])
101 print (tabulate(data2.head(10),headers='keys'))

    country       income    alcohol    life
--  ----------  --------  ---------  ------
1  Albania            1       7.29  76.918
2  Algeria            1       0.69  73.131
4  Angola             1       5.57  51.093
6  Argentina          3       9.35  75.901
7  Armenia            1      13.66  74.241
9  Australia          4      10.21  81.907
10 Austria            4      12.4   80.854
11 Azerbaijan         1      13.34  70.739
12 Bahamas            3       8.65  75.62
13 Bahrain            3       4.19  75.057

103 data2['life'] = pd.cut(data1.life,[40,50,60,70,80,90], labels=['1','2','3','4','5'])
104 print (tabulate(data2.head(10),headers='keys'))

    country       income    alcohol    life
--  ----------  --------  ---------  ------
1  Albania            1       7.29       4
2  Algeria            1       0.69       4
4  Angola             1       5.57       2
6  Argentina          3       9.35       4
7  Armenia            1      13.66       4
9  Australia          4      10.21       5
10 Austria            4      12.4        5
11 Azerbaijan         1      13.34       4
12 Bahamas            3       8.65       4
13 Bahrain            3       4.19       4

106 data2['alcohol'] = pd.cut(data1.alcohol,[0.5,5,10,15,20,25], labels=['1','2','3','4','5'])
107 print (tabulate(data2.head(10),headers='keys'))

    country       income    alcohol    life
--  ----------  --------  ---------  ------
1  Albania            1          2       4
2  Algeria            1          1       4
4  Angola             1          2       2
6  Argentina          3          2       4
7  Armenia            1          3       4
9  Australia          4          3       5
10 Austria            4          3       5
11 Azerbaijan         1          3       4
12 Bahamas            3          2       4
13 Bahrain            3          1       4
````

### [Categorical Frequency Distributions](#freq2)
The lines 109-137 showed the absolute and relative frequencies distributions for the new categorical variables.

````python

109 # absolute Frequency distributions
110 freq_life_n = data2.life.value_counts(sort=False)
111 freq_income_n = data2.income.value_counts(sort=False)
112 freq_alcohol_n = data2.alcohol.value_counts(sort=False)
113
114 # Relative Frequency distributions
115 freq_life_r = data2.life.value_counts(sort=False, normalize=True)
116 freq_income_r = data2.income.value_counts(sort=False, normalize=True)
117 freq_alcohol_r = data2.alcohol.value_counts(sort=False, normalize=True)
118
119 print ('************************')
120 print ('* Absolute Frequencies *')
121 print ('************************')
122 print ('\nlife variable ('+LIFE+'):')
123 print( tabulate([freq_life_n], tablefmt="fancy_grid", headers=(life_map.values())))
124 print ('\nincome variable ('+INCOME+'):')
125 print( tabulate([freq_income_n], tablefmt="fancy_grid", headers=(income_map.values())))
126 print ('\nalcohol variable ('+ALCOHOL+'):')
127 print( tabulate([freq_alcohol_n], tablefmt="fancy_grid", headers=(alcohol_map.values())))
128
129 print ('\n************************')
130 print ('* Relative Frequencies *')
131 print ('************************')
132 print ('\nlife variable ('+LIFE+'):')
133 print( tabulate([freq_life_r], tablefmt="fancy_grid", headers=(life_map.values())))
134 print ('\nincome variable ('+INCOME+'):')
135 print( tabulate([freq_income_r], tablefmt="fancy_grid", headers=(income_map.values())))
136 print ('\nalcohol variable ('+ALCOHOL+'):')
137 print( tabulate([freq_alcohol_r], tablefmt="fancy_grid", headers=(alcohol_map.values())))

************************
* Absolute Frequencies *
************************

life variable (Expectancy life):
╒════════════╤════════════╤════════════╤════════════╤════════════╕
│   >=40 <50 │   >=50 <60 │   >=60 <70 │   >=70 <80 │   >=80 <90 │
╞════════════╪════════════╪════════════╪════════════╪════════════╡
│          8 │         28 │         35 │         80 │         20 │
╘════════════╧════════════╧════════════╧════════════╧════════════╛

income variable (Income):
╒══════════════╤═════════════╤══════════════╤══════════════╤══════════════╤══════════════╕
│   >=100  <5k │   >=5k <10k │   >=10k <20k │   >=20K <30K │   >=30K <40K │   >=40K <50K │
╞══════════════╪═════════════╪══════════════╪══════════════╪══════════════╪══════════════╡
│          110 │          24 │           15 │           12 │            9 │            0 │
╘══════════════╧═════════════╧══════════════╧══════════════╧══════════════╧══════════════╛

alcohol variable (Alchohol):
╒════════════╤═══════════╤════════════╤════════════╤════════════╕
│   >=0.5 <5 │   >=5 <10 │   >=10 <15 │   >=15 <20 │   >=20 <25 │
╞════════════╪═══════════╪════════════╪════════════╪════════════╡
│         63 │        56 │         31 │         10 │          1 │
╘════════════╧═══════════╧════════════╧════════════╧════════════╛

************************
* Relative Frequencies *
************************

life variable (Expectancy life):
╒════════════╤════════════╤════════════╤════════════╤════════════╕
│   >=40 <50 │   >=50 <60 │   >=60 <70 │   >=70 <80 │   >=80 <90 │
╞════════════╪════════════╪════════════╪════════════╪════════════╡
│  0.0467836 │   0.163743 │   0.204678 │   0.467836 │   0.116959 │
╘════════════╧════════════╧════════════╧════════════╧════════════╛

income variable (Income):
╒══════════════╤═════════════╤══════════════╤══════════════╤══════════════╤══════════════╕
│   >=100  <5k │   >=5k <10k │   >=10k <20k │   >=20K <30K │   >=30K <40K │   >=40K <50K │
╞══════════════╪═════════════╪══════════════╪══════════════╪══════════════╪══════════════╡
│     0.647059 │    0.141176 │    0.0882353 │    0.0705882 │    0.0529412 │            0 │
╘══════════════╧═════════════╧══════════════╧══════════════╧══════════════╧══════════════╛

alcohol variable (Alchohol):
╒════════════╤═══════════╤════════════╤════════════╤════════════╕
│   >=0.5 <5 │   >=5 <10 │   >=10 <15 │   >=15 <20 │   >=20 <25 │
╞════════════╪═══════════╪════════════╪════════════╪════════════╡
│   0.391304 │  0.347826 │   0.192547 │  0.0621118 │ 0.00621118 │
╘════════════╧═══════════╧════════════╧════════════╧════════════╛
````
[Full Code](#full_code)
```python
1 # coding: utf-8
2 import pandas as pd
3 import numpy as np
4 from collections import OrderedDict
5 from tabulate import tabulate, tabulate_formats
6
7 # bug fix for display formats to avoid run time errors
8 pd.set_option('display.float_format', lambda x:'%f'%x)
9
10 # Load from CSV
11 data1 = pd.read_csv('gapminder.csv', skip_blank_lines=True,
12                     usecols=['country','incomeperperson', 'alcconsumption', 'lifeexpectancy'])
13                     
14 # Rename columns for clarity
15 data1.columns = ['country','income','alcohol','life']
16
17 # Variables Descriptions
18 ALCOHOL = "2008 alcohol consumption per adult (liters, age 15+)"
19 INCOME = "2010 Gross Domestic Product per capita in constant 2000 US$"
20 LIFE = "2011 life expectancy at birth (years)"
21
22 # Show info about dataset
23 data1.info()
24
25 # converting to numeric values and parsing
26 for dt in ('income','alcohol','life') :
27    data1[dt] = pd.to_numeric(data1[dt], 'errors=coerce')
28    
29 print (data1.info())
30
31 # Missing values, just for curiosity
32 xdata1 = data1[data1.income.isnull() | data1.life.isnull() | data1.alcohol.isnull() | data1.country.isnull()]
33 print (tabulate(xdata1.head(10), headers=['index','Country','Income','Alcohol','Life']))
34
35 # remove rows with nan values
36 data1 = data1.dropna(axis=0, how='any')
37 print (data1.info())
38
39 # absolute Frequency distributions
40 freq_life_n = data1.life.value_counts(sort=False)
41 freq_income_n = data1.income.value_counts(sort=False)
42 freq_alcohol_n = data1.alcohol.value_counts(sort=False)
43
44 # Relative Frequency distributions
45 freq_life_r = data1.life.value_counts(sort=False, normalize=True)
46 freq_income_r = data1.income.value_counts(sort=False, normalize=True)
47 freq_alcohol_r = data1.alcohol.value_counts(sort=False, normalize=True)
48
49 print ('********************************************************')
50 print ('* Absolute Frequencies original variables (first 5)    *')
51 print ('********************************************************')
52 print ('\nlife variable ('+LIFE+'):')
53 print ( tabulate([freq_life_n.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_life_n.index])) )
54 print ('\nincome variable ('+INCOME+'):')
55 print ( tabulate([freq_income_n.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_income_n.index])) )
56 print ('\nalcohol variable ('+ALCOHOL+'):')
57 print ( tabulate([freq_life_n.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_life_n.index])) )
58
59 print ('\n********************************************************')
60 print ('* Relative Frequencies original variables (first 5)    *')
61 print ('********************************************************')
62
63 print ('\nlife variable ('+LIFE+'):')
64 print ( tabulate([freq_life_r.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_life_n.index])) )
65 print ('\nincome variable ('+INCOME+'):')
66 print ( tabulate([freq_income_r.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_income_n.index])) )
67 print ('\nalcohol variable ('+ALCOHOL+'):')
68 print ( tabulate([freq_life_r.head(5)], tablefmt="fancy_grid", headers=([i for i in freq_life_n.index])) )
69
70 # Min and Max continuous variables:
71 min_max = OrderedDict()
72 dict1 = OrderedDict()
73
74 dict1['min'] = data1.life.min()
75 dict1['max'] = data1.life.max()
76 min_max['life'] = dict1
77
78 dict2 = OrderedDict()
79 dict2['min'] = data1.income.min()
80 dict2['max'] = data1.income.max()
81 min_max['income'] = dict2
82
83 dict3 = OrderedDict()
84 dict3['min'] = data1.alcohol.min()
85 dict3['max'] = data1.alcohol.max()
86 min_max['alcohol'] = dict3
87
88 df = pd.DataFrame([min_max['income'],min_max['life'],min_max['alcohol']], index = ['Income','Life','Alcohol'])
89 print (tabulate(df.sort_index(axis=1, ascending=False), headers=['Var','Min','Max']))
90
91
92 data2 = data1.copy()
93
94 # Maps
95 income_map = {1: '>=100  <5k', 2: '>=5k <10k', 3: '>=10k <20k',
95 income_map = {1: '>=100  <5k', 2: '>=5k <10k', 3: '>=10k <20k',
96               4: '>=20K <30K', 5: '>=30K <40K', 6: '>=40K <50K' }
97 life_map = {1: '>=40 <50', 2: '>=50 <60', 3: '>=60 <70', 4: '>=70 <80', 5: '>=80 <90'}
98 alcohol_map = {1: '>=0.5 <5', 2: '>=5 <10', 3: '>=10 <15', 4: '>=15 <20', 5: '>=20 <25'}
99
100 data2['income'] = pd.cut(data1.income,[100,5000,10000,20000,30000,40000,50000], labels=['1','2','3','4','5','6        '])
101 print (tabulate(data2.head(10),headers='keys'))
102
103 data2['life'] = pd.cut(data1.life,[40,50,60,70,80,90], labels=['1','2','3','4','5'])
104 print (tabulate(data2.head(10),headers='keys'))
105
106 data2['alcohol'] = pd.cut(data1.alcohol,[0.5,5,10,15,20,25], labels=['1','2','3','4','5'])
107 print (tabulate(data2.head(10),headers='keys'))
108
109 # absolute Frequency distributions
110 freq_life_n = data2.life.value_counts(sort=False)
111 freq_income_n = data2.income.value_counts(sort=False)
112 freq_alcohol_n = data2.alcohol.value_counts(sort=False)
113
114 # Relative Frequency distributions
115 freq_life_r = data2.life.value_counts(sort=False, normalize=True)
116 freq_income_r = data2.income.value_counts(sort=False, normalize=True)
117 freq_alcohol_r = data2.alcohol.value_counts(sort=False, normalize=True)
118
119 print ('************************')
120 print ('* Absolute Frequencies *')
121 print ('************************')
122 print ('\nlife variable ('+LIFE+'):')
123 print( tabulate([freq_life_n], tablefmt="fancy_grid", headers=(life_map.values())))
124 print ('\nincome variable ('+INCOME+'):')
125 print( tabulate([freq_income_n], tablefmt="fancy_grid", headers=(income_map.values())))
126 print ('\nalcohol variable ('+ALCOHOL+'):')
127 print( tabulate([freq_alcohol_n], tablefmt="fancy_grid", headers=(alcohol_map.values())))
128
129 print ('\n************************')
130 print ('* Relative Frequencies *')
131 print ('************************')
132 print ('\nlife variable ('+LIFE+'):')
133 print( tabulate([freq_life_r], tablefmt="fancy_grid", headers=(life_map.values())))
134 print ('\nincome variable ('+INCOME+'):')
135 print( tabulate([freq_income_r], tablefmt="fancy_grid", headers=(income_map.values())))
136 print ('\nalcohol variable ('+ALCOHOL+'):')
137 print( tabulate([freq_alcohol_r], tablefmt="fancy_grid", headers=(alcohol_map.values())))
```
