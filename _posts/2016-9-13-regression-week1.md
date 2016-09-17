---
layout: post
title: Regression Modeling in Practice - Week1 | Introduction to Regression Interactions
published: true
---

This is the first assignment or the third course (of five)
[Data Analysis and Interpretation Specialization]
(https://www.coursera.org/specializations/data-analysis)
detailed information about it can be seeing
[here](https://www.coursera.org/learn/data-visualization#).

## Assignment 4:
The third assignment deals with how write about data ("one of the
most important skills of data-analysis").

### Index
+ [Variables](#variables)
+ [Income](#income)
+ [Life](#life)
+ [Alcohol](#alcohol)
+ [Conclusion](#conclusion)

### <a name = "variables"></a>Variables

Details of my project can be seeing
[here](https://sidon.github.io/data-visualization-week1/), to get easier,
I made a summary bellow:

|Variable Name|Description|
|-------------|-----------|
|Income       |moderator: GPD per capita (1)|
|Life         |Explanatory Variable: Life Expectancy (2)|
|Alcohol      |Response Varialbe: Alcohol Consumption (3)|

(1) 2010 Gross Domestic Product per capita in constant 2000 US$"

(2) 2011 life expectancy at birth (years)

(3) 2008 alcohol consumption per adult (liters, age 15+)

### <a name = "income"></a>Income per Person

GDP is published in a country’s National Accounts. These statistics comply to protocols laid down in the 1993 version of the Systems of National Accounts, SNA93.
The GDP calculation methodology can be seen [here](http://www.geostat.ge/cms/site_images/_files/english/methodology/GDP%20Brief%20Methodology%20ENG.pdf)

#### Sample and procedure
[The primary World Bank collection of development indicators](http://data.worldbank.org/data-catalog/world-development-indicators), compiled from officially-recognized international sources. It presents the most current and accurate global development data available, and includes national, regional and global estimates.
Type: Time Series, Periodicity: Annual  This study: 2010, Number of countries: 246

### <a name = "life"></a>Life Expectancy
The data was provided mainly, by [Human Mortality Database] (http://www.mortality.org/)
The Human Mortality Database (HMD) was created to provide detailed mortality and population data to researchers, students, journalists, policy analysts, and others interested in the history of human longevity. The project began as an outgrowth of earlier projects in the Department of Demography at the University of California, Berkeley, USA, and at the Max Planck Institute for Demographic Research in Rostock, Germany (see history). It is the work of two teams of researchers in the USA and Germany (see research teams), with the help of financial backers and scientific collaborators from around the world (see acknowledgements). The French Institute for Demographic Studies (INED) has also supported the further development of the database in recent years.

#### Sample and procedure
The Human Mortality Database (HMD) contains uniform death rates and life tables (e.g., life expectancy) for various populations. It also includes the original raw data (i.e., births, deaths, census counts or official population estimates) from which they were derived. For a detailed description about methods and data about data,
see [here](http://www.mortality.org/Public/Docs/MP-Summary.pdf) and
[here](http://www.mortality.org/Public/Docs/MP-Summary.pdf)


### <a name = "Alcohol"></a>Alcohol consumption per adult (age 15+)

In this work, the data are from 2008 and refer to  alcohol consumption per adult (age 15+), litres Recorded and estimated average alcohol consumption, adult (15+) per capita consumption in litres pure alcohol, this database were provided by [World Health Organization] (http://www.who.int/en/) through the Global status report on alcohol and health. This report presents a comprehensive perspective on the global, regional and country consumption of alcohol, patterns of
drinking, health consequences and policy responses in Member States. It represents a continuing effort by the World Health Organization (WHO) to support Member States in collecting information in order to assist them in their efforts to reduce the harmful use of alcohol, and its health and social consequences.

#### Sample and procedure
The Global status report on alcohol and health have 286 page, the description about data sources and the methodology can be seen in approximately ten pages (Appendix IV. pg. 279
Data sources and methods) [on this pdf]
 (http://www.who.int/substance_abuse/publications/global_alcohol_report/msbgsruprofiles.pdf)


### <a name = "conclusion"></a>Conclusion

My code book was prepared  from [GapMinder](https://d396qusza40orc.cloudfront.net/phoenixassets/data-management-visualization/GapMinder%20Codebook%20.pdf), the data that I chose are provided from various sources,
some of them provided by governments of countries,
in the case of GPD (income per person), unfortunately, was not possible to found some information that could make this work richer.
