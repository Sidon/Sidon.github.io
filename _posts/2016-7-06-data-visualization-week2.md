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
2 import pandas as pd
3 import numpy
4 from collections import OrderedDict
5 from tabulate import tabulate, tabulate_formats
6
7 # Dictionaries
8 counts = OrderedDict()
9 prcnts = OrderedDict()
10
11 # Load from CSV
12 data1 = pd.read_csv('gapminder.csv', skip_blank_lines=True,
13                     usecols=['country','incomeperperson',
14                              'alcconsumption', 'lifeexpectancy'])
15
16 # Rename columns for clarity
17 data1.columns = ['country','ipp','ac','le']
18
19 # Show info about pandas dataframe
20 data1.info()
21
22 # Counts missing entry in ipp, ac and le
23 # --------------------------------------
24 missings = [['Var', 'Missings']]
25 for var in ('ipp', 'ac', 'le'):
26     missings.append([var, data1[var].value_counts()[' ']])
27
28 print (tabulate(missings, headers="firstrow"))
29
30 # Count each variable (coerce’, then invalid parsing will be set as NaN)
31 for dt in ('ipp','ac', 'le') :
32     counts[dt] = pd.to_numeric(data1[dt], 'errors=coerce')
33
34 print (counts['ipp'])
35 print (counts['ac'])
36 print (counts['le'])
37
38 # each variable as percentage
39 for dt in ('ipp','ac', 'le') :
40     prcnts[dt] = data1[dt].value_counts(sort=False, normalize=True)
41
42 print (prcnts['ipp'])
43 print (prcnts['ac'])
44 print (prcnts['le'])
````

### The output and explanation
As my variables do not represent categories, maybe the frequency distributions do not seem to make sense, anyhow they are showed on the lines 42-44.

#### Line 20 (Data set info)
This line shows information about dataset, where:  
ipp = incomeperperson  
ac = alcconsumption  
le = lifeexpectancy  

Clique [here](https://sidon.github.io/data-visualization-week1/) seeing original names on the codebook.

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

#### Line 28 (Data missing)
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

#### Line 34 (ipp nominal frequency)
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

#### Line 35 (ac nominal frequency)
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

#### Line 36 (le nominal frequency)
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

#### Line 42 (ipp frequency expressed as a percentage)
This line shows the frequency values, of each observation related to the variable ipp, expressed as a percentage.

```python
print (prcnts['ipp'])
1621.17707762392    0.004695
26692.9841066319    0.004695
19630.5405471267    0.004695
39309.4788585145    0.004695
2636.78779985257    0.004695
591.06794433684     0.004695
1860.75389496662    0.004695
609.131205921911    0.004695
5332.23859142075    0.004695
456.385711651118    0.004695
242.677534160129    0.004695
184.141796591644    0.004695
7381.31275080681    0.004695
1232.79413697982    0.004695
3233.42378012982    0.004695
1714.94288994653    0.004695
1543.95645667048    0.004695
9243.58705259742    0.004695
6147.77960984301    0.004695
338.266391227048    0.004695
2534.00037997061    0.004695
1258.76259631224    0.004695
3745.64985213146    0.004695
5184.70932756049    0.004695
2425.4712932681     0.004695
268.331790297681    0.004695
2667.24670973056    0.004695
1326.74175718861    0.004695
1253.29201505445    0.004695
155.033231230204    0.004695
                      ...   
15313.8593472276    0.004695
                    0.107981
161.317137104969    0.004695
12505.2125447354    0.004695
2222.33505218301    0.004695
3164.9276932512     0.004695
180.083376000006    0.004695
37491.1795229012    0.004695
1381.00426770244    0.004695
275.884286531631    0.004695
25306.1871926737    0.004695
495.734246943527    0.004695
6334.10519399913    0.004695
760.262365036505    0.004695
2344.89691619809    0.004695
33923.3138682688    0.004695
557.947512595975    0.004695
5182.14372064153    0.004695
1194.71143337515    0.004695
3180.43061177196    0.004695
1914.99655094922    0.004695
15822.1121405699    0.004695
1144.10219337041    0.004695
4189.43658749046    0.004695
1036.830724903      0.004695
39972.3527684608    0.004695
4699.41126207406    0.004695
9106.32723421876    0.004695
37662.751249706     0.004695
354.599726291282    0.004695
Name: ipp, dtype: float64
```

#### Line 43 (ac frequency expressed as a percentage)
This line shows the frequency values, of each observation related to the variable ac, expressed as a percentage.

```python
print (prcnts['ac'])
1.54     0.004695
16.47    0.004695
7.6      0.004695
1.29     0.004695
4.99     0.004695
5.25     0.004695
8.65     0.004695
.69      0.004695
10.21    0.004695
.1       0.009390
8.94     0.004695
2.69     0.004695
.65      0.004695
10.62    0.004695
16.12    0.004695
5.81     0.004695
6.16     0.004695
9.46     0.004695
10.71    0.004695
10.16    0.004695
3.91     0.004695
6.28     0.004695
1.32     0.004695
5.56     0.009390
7.3      0.004695
9.6      0.004695
8.99     0.004695
6.08     0.004695
.32      0.004695
6.47     0.004695
           ...   
.2       0.004695
         0.122066
8.45     0.004695
15       0.004695
.92      0.004695
.52      0.004695
16.23    0.004695
2.52     0.004695
.5       0.004695
1.05     0.004695
4.81     0.004695
9.86     0.004695
9.65     0.004695
3.9      0.004695
11.83    0.004695
3.56     0.004695
14.92    0.004695
4.19     0.004695
1.49     0.004695
14.43    0.004695
3.92     0.004695
3.23     0.004695
4.71     0.004695
3.64     0.004695
5.78     0.004695
9.99     0.009390
12.48    0.004695
13.45    0.004695
7.08     0.004695
1.44     0.004695
Name: ac, dtype: float64
```

#### Line 44 (le frequency expressed as a percentage)
This line shows the frequency values, of each observation related to the variable le, expressed as a percentage.

```python
print (prcnts['le'])

73.456    0.004695
77.685    0.004695
73.403    0.004695
70.349    0.004695
79.634    0.004695
55.439    0.004695
55.442    0.004695
71.172    0.004695
71.017    0.004695
75.901    0.004695
57.937    0.004695
75.956    0.004695
78.005    0.004695
81.539    0.004695
74.515    0.004695
67.852    0.004695
74.788    0.004695
80.557    0.004695
51.088    0.004695
74.576    0.004695
73.737    0.004695
74.241    0.004695
74.044    0.004695
79.591    0.004695
54.21     0.004695
75.133    0.004695
53.183    0.004695
79.963    0.004695
72.444    0.004695
65.193    0.004695
            ...   
80.414    0.004695
          0.103286
73.131    0.004695
58.582    0.004695
48.718    0.004695
62.095    0.004695
68.287    0.004695
81.618    0.004695
81.097    0.004695
83.394    0.004695
67.714    0.004695
74.522    0.004695
73.703    0.004695
73.371    0.004695
73.396    0.004695
74.126    0.004695
72.477    0.004695
48.397    0.004695
70.739    0.004695
81.804    0.004695
73.235    0.004695
65.493    0.004695
72.231    0.004695
72.974    0.009390
73.99     0.004695
82.759    0.004695
49.025    0.004695
68.494    0.004695
75.62     0.004695
61.061    0.004695
Name: le, dtype: float64
```
