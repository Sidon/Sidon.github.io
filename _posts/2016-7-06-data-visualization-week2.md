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
561.708585      1
2668.020519     1
5634.003948     1
6147.779610     1
772.933345      1
1975.551906     1
1543.956457     1
13577.879885    1
15461.758372    1
523.950151      1
33923.313868    1
30532.277044    1
5900.616944     1
20751.893424    1
786.700098      1
275.884287      1
276.200413      1
4885.046701     1
1144.102193     1
1784.071284     1
369.572954      1
9243.587053     1
285.224449      1
37662.751250    1
544.599477      1
37491.179523    1
180.083376      1
1525.780116     1
39972.352768    1
18982.269285    1
               ..
5348.597192     1
12505.212545    1
62682.147006    1
161.317137      1
220.891248      1
952.827261      1
32535.832512    1
736.268054      1
371.424198      1
9425.325870     1
1253.292015     1
27110.731591    1
25575.352623    1
744.239413      1
2025.282665     1
1258.762596     1
8445.526689     1
5188.900935     1
32292.482984    1
239.518749      1
25306.187193    1
5528.363114     1
242.677534      1
2534.000380     1
16372.499781    1
2549.558474     1
760.262365      1
31993.200694    1
22275.751661    1
10749.419238    1
Name: income, dtype: int64
```

#### Line 35 (ac nominal frequency)
This line shows the nominal values of frequency of each observation related to the variable ac.

```python
print (counts['ac'])
0.690000     1
0.540000     1
2.080000     1
3.170000     1
4.190000     1
5.570000     1
6.420000     1
7.290000     1
8.170000     1
9.350000     1
10.170000    1
11.400000    1
12.400000    1
13.660000    1
0.790000     1
15.000000    1
16.470000    1
17.240000    1
18.850000    1
1.870000     1
12.090000    1
0.500000     1
3.880000     1
23.010000    1
8.450000     1
0.960000     1
5.070000     1
2.560000     1
3.990000     1
0.110000     1
            ..
5.120000     1
8.690000     1
12.050000    1
2.520000     1
0.170000     1
1.490000     1
1.050000     1
11.830000    1
13.100000    1
0.870000     1
0.340000     2
9.990000     2
9.430000     1
6.560000     1
5.000000     1
14.940000    1
4.100000     2
7.300000     1
7.600000     1
1.320000     1
2.700000     1
5.170000     1
4.990000     1
11.410000    1
1.440000     1
3.920000     1
2.270000     1
3.640000     1
6.280000     1
10.080000    1
Name: alcohol, dtype: int64
```

#### Line 36 (le nominal frequency)
This line shows the nominal values of frequency of each observation related to the variable le.

```python
print (counts['le'])

```

#### Line 42 (ipp frequency expressed as a percentage)
This line shows the frequency values, of each observation related to the variable ipp, expressed as a percentage.

```python
print (prcnts['ipp'])
80.170000    1
74.402000    1
74.576000    1
57.937000    1
76.546000    1
69.317000    1
73.456000    1
77.653000    1
73.737000    1
58.582000    1
74.847000    1
79.591000    1
73.127000    1
75.181000    1
73.339000    1
62.095000    1
61.452000    1
73.990000    1
80.934000    1
76.072000    1
72.832000    1
72.283000    1
62.703000    1
75.446000    1
68.823000    1
74.044000    1
79.634000    1
76.652000    1
61.597000    1
47.794000    1
            ..
72.317000    1
72.477000    1
81.804000    1
80.009000    1
68.749000    1
73.911000    1
75.632000    1
48.196000    1
57.062000    1
62.465000    1
74.522000    1
81.097000    1
68.498000    1
69.042000    1
81.404000    1
75.620000    1
79.341000    1
76.142000    1
80.557000    1
58.199000    1
68.287000    1
79.915000    1
55.377000    1
50.239000    1
59.318000    1
74.126000    1
74.825000    1
76.128000    1
72.231000    1
56.786000    1
Name: life, dtype: int64
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
