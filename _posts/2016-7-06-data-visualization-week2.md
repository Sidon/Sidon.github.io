---
layout: post
title: Data Visualization - Week 2
published: true
---

This is the second week of the course, in this week the students have to choose the language/tool to work (SaS or Python) and develop the first program based on their project, my chose was [Python](https://www.python.org/) and bellow I presented the assignment.

## Assignment 2:
On this assignment, the program must load the dataset into memory and calculate the frequency distributions for chosen variables.

Bellow there is my code:

````python
1 # coding: utf-8
2
3 import pandas as pd
4 import numpy
5 from collections import OrderedDict
6 from tabulate import tabulate, tabulate_formats
7
8 # Dictionares
9 counts = OrderedDict()
10 prcnts = OrderedDict()
11
12 # Load from CSV
13 data1 = pd.read_csv('gapminder.csv', skip_blank_lines=True,
14                     usecols=['country','incomeperperson',
15                      'alcconsumption', 'lifeexpectancy'])
16  
17 # Rename columns for clarity                                    
18 data1.columns = ['country','ipp','ac','le']
19
20 # Show info about pandas dataframe
21 data1.info()
22
23 # Counts missing entry in ipp, ac and le
24 from tabulate import tabulate, tabulate_formats
25 missings = [['Var', 'Missings']]
26 for var in ('ipp', 'ac', 'le'):
27     missings.append([var, data1[var].value_counts()[' ']])
28    
29 print (tabulate(missings, headers="firstrow"))
30
31 # Count each variable (coerce’, then invalid parsing will be set as NaN)
32 for dt in ('ipp','ac', 'le') :
33     counts[dt] = pd.to_numeric(data1[dt], 'errors=coerce')
34
35 # Count each variable (coerce’, then invalid parsing will be set as NaN)
36 for dt in ('ipp','ac', 'le') :
37     counts[dt] = pd.to_numeric(data1[dt], 'errors=coerce')
38
39 print (counts['ipp'])
40 print (counts['ac'])
41 print (counts['le'])
42
43 # percent each variable
44 for dt in ('ipp','ac', 'le') :
45     prcnts[dt] = data1[dt].value_counts(sort=False, normalize=True)
46
47 print (prcnts['ipp'])
48 print (prcnts['ac'])
49 print (prcnts['le'])
````

## The output and explanation:

#### Line 21 (Data set info)
This line shows information about dataset, where:  
ipp = incomeperperson  
ac = alcconsumption  
le = lifeexpectancy  

````python    
data1.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 213 entries, 0 to 212
Data columns (total 4 columns):
country    213 non-null object
ipp        213 non-null object
ac         213 non-null object
le         213 non-null object
dtypes: object(4)
memory usage: 6.7+ KB
````

#### Line 29 (Data missing)
Though the information showed by the function info() in line 21 might appear that there is not missing data, this is not true, because missing information in this dataset is a space (a non-null value), thus in the lines, 23-29 is showed the number of missing data for  each variable by value_counts() function.

````python  
missings = [['Var', 'Missings']]
for var in ('ipp', 'ac', 'le'):
    missings.append([var, data1[var].value_counts()[' ']])

print (tabulate(missings, headers="firstrow"))
Var      Missings
-----  ----------
ipp            23
ac             26
le             22
````

### Line 39
This line shows the nominal values of frequency of each observation related to the variable ipp.

```python
print (counts['ipp'])
0               NaN
1       1914.996551
2       2231.993335
3      21943.339898
4       1381.004268
5      11894.464075
6      10749.419238
7       1326.741757
8               NaN
9      25249.986061
10     26692.984107
11      2344.896916
12     19630.540547
13     12505.212545
14       558.062877
15      9243.587053
16      2737.670379
17     24496.048264
18      3545.652174
19       377.039699
20     62682.147006
21      1324.194906
22      1232.794137
23      2183.344867
24      4189.436587
25      4699.411262
26     17092.460004
27      2549.558474
28       276.200413
29       115.305996
           ...     
183     1810.230533
184    32292.482984
185    37662.751250
186     1525.780116
187             NaN
188      279.180453
189      456.385712
190     2712.517199
191      369.572954
192      285.224449
193     2025.282665
194    10480.817203
195     3164.927693
196     5348.597192
197     2062.125152
198     1714.942890
199      377.421113
200     1036.830725
201    21087.394125
202    28033.489283
203    37491.179523
204     9106.327234
205      952.827261
206     1543.956457
207     5528.363114
208      722.807559
209             NaN
210      610.357367
211      432.226337
212      320.771890
Name: ipp, dtype: float64
```

### Line 40
This line shows the nominal values of frequency of each observation related to the variable ac.

```python
print (counts['ac'])
0       0.03
1       7.29
2       0.69
3      10.17
4       5.57
5       8.17
6       9.35
7      13.66
8        NaN
9      10.21
10     12.40
11     13.34
12      8.65
13      4.19
14      0.17
15      6.42
16     18.85
17     10.41
18      5.92
19      2.08
20       NaN
21      0.54
22      5.78
23      9.60
24      6.97
25     10.08
26      1.86
27     11.40
28      7.32
29      9.65
       ...  
183     5.05
184     9.50
185    11.41
186     1.49
187      NaN
188     3.39
189     7.86
190     7.08
191     0.74
192     1.92
193     3.92
194     6.16
195     1.05
196     3.02
197     5.00
198     2.14
199    16.40
200    17.47
201     0.52
202    13.24
203     9.70
204     8.99
205     3.61
206     0.96
207     7.60
208     3.91
209      NaN
210     0.20
211     3.56
212     4.96
Name: ac, dtype: float64
```

### Line 41
This line shows the nominal values of frequency of each observation related to the variable le.

```python
print (counts['le'])
0      48.673
1      76.918
2      73.131
3         NaN
4      51.093
5         NaN
6      75.901
7      74.241
8      75.246
9      81.907
10     80.854
11     70.739
12     75.620
13     75.057
14     68.944
15     76.835
16     70.349
17     80.009
18     76.072
19     56.081
20        NaN
21     67.185
22     66.618
23     75.670
24     53.183
25     73.488
26     78.005
27     73.371
28     55.439
29     50.411
        ...  
183    48.718
184    81.439
185    82.338
186    75.850
187       NaN
188    67.529
189    58.199
190    74.126
191    62.475
192    57.062
193    72.317
194    70.124
195    74.515
196    73.979
197    64.986
198       NaN
199    54.116
200    68.494
201    76.546
202    80.170
203    78.531
204    77.005
205    68.287
206    71.017
207    74.402
208    75.181
209    72.832
210    65.493
211    49.025
212    51.384
Name: le, dtype: float64
```
