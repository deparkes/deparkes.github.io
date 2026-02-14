---
layout: post
title: UK Rainfall Data
date: 2021-06-18 18:47:02.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- analysis
- climate
- climate change
- data
- pandas
- processing
- python
- rainfall
author: deparkes
permalink: "/2021/06/18/uk-rainfall-data/"
---
<h2>Historic UK Rainfall Data</h2>
The Met Office Hadley Centre holds (<a href="https://www.metoffice.gov.uk/hadobs/hadukp/">Met Office Hadley Centre observations datasets HadUKP</a>) UK Rainfall Data going back to the 1800s. It records the daily average rain fall for 9 regions around England, Wales, Scotland and Northern Ireland.
You can download the data from here: <a href="https://www.metoffice.gov.uk/hadobs/hadukp/data/download.html">Met Office Hadley Centre HadUKP Data Download</a>
See terms and conditions for using this data: <a href="https://www.metoffice.gov.uk/hadobs/hadukp/terms_and_conditions.html">Met Office Hadley Centre hadukp observations datasets</a>
<h3>Exploring Daily Total Rainfall</h3>
One of the more granular sources provided by the Hadley Centre is daily rainfall totals for each region. You can download the individual files from the website, but unfortunately it looks like their robots.txt prevents programmatic downloading of the files.
Once downloaded you can use pandas read_csv to load the data into a pandas dataframe.  A couple of things to watch out for though:
<ul>
<li>Skipping the first few rows and specifying that there is no header row. See <a href="https://www.edureka.co/community/42836/how-to-read-pandas-csv-file-with-no-header">here</a> for how to get around that.</li>
<li>Using more than one space character as a column separator. See <a href="https://stackoverflow.com/questions/15026698/how-to-make-separator-in-pandas-read-csv-more-flexible-wrt-whitespace-for-irreg">here</a> for how to get around that.</li>
<li>Handling NA values (which are set as -99.99 and mess up calculations). See <a href="https://www.geeksforgeeks.org/use-of-na_values-parameter-in-read_csv-function-of-pandas-in-python/">here</a> for how to get around that.</li>
</ul>
The full line I used was:

```python
df = pd.read_csv('data/HadSWEP_daily_qc.txt', sep=r'\s+', skiprows=3, skipinitialspace=True, header=None, na_values=-99.99)
```

Since the file did not come with its own header columns I added them after loading the file. I also added a column for region so that multiple regions could be handled at once if necessary ('SEEP' is from the original data file and means 'South East England Precipitation').

```python
df.columns = ['year', 'month']+ [i+1 for i in range(31)]
df['region'] = 'SEEP'
```

The data table provided is in a 'wide' format with a column for each day of the month. This is helpful for human-readability, but isn't so good for computer processing. To convert for a 'wide' to a 'long' form table we can use the 'melt' pandas method.
<a href="{{site.url}}/2016/10/28/reshape-pandas-data-with-melt/">Read more about pandas melt</a>

```python
melted = pd.melt(df, id_vars=['region', 'year', "month"],
                 var_name="day", value_name="rainfall")
```

<h3>Example Analysis</h3>
The melted dataframe is in a good place to do further analysis and get a feel for what is possible.
<h4>How Much Rain Will There Be?</h4>
We can attempt to estimate how much rain there will be on a given day of the year by looking at that average for that day. This isn't really forecasting, but it does help you know generally how rainy a given day of the year might be.

```python
df2 = melted[melted['region']=='SEEP'].groupby(['month', 'day'])['rainfall'].mean()
```

We can plot this new grouped dataframe and confirm that the trends to at least seem to mostly make sense: the summer is relatively dry and the winter is relatively wet.

| ![UK Rainfall Data - average daily rainfal]({{site.url}}/assets/2021/06/AverageDailyRainfall.png) |
|:--:|
| *UK Rainfall Data - average daily rainfal* |

Having the mean rainfall is one thing, but often we want to dig a bit deeper than that. We can easily extend our initial 'mean' calculation to include maximum, minimum and standard deviation of rainfall measurements.
<a href="https://stackoverflow.com/questions/12589481/multiple-aggregations-of-the-same-column-using-pandas-groupby-agg">Read more about multiple aggregations </a>and also <a href="https://pandas-docs.github.io/pandas-docs-travis/user_guide/groupby.html#named-aggregation">here</a>

```python
import numpy as np
df3 = melted[melted['region']=='SEEP'].groupby(['month', 'day']).agg(
    mean_rain=pd.NamedAgg(column='rainfall', aggfunc='mean'),
    max_rain=pd.NamedAgg(column='rainfall', aggfunc='max'),
    min_rain=pd.NamedAgg(column='rainfall', aggfunc='min'),
    std=pd.NamedAgg(column='rainfall', aggfunc=np.std),
)
df4 = df3.reset_index()
df4.head()
```

<h3>How Likely Is it to Rain?</h3>
We can also use this historic UK rainfall data to give some estimate as to the chance of rain on a given day. I want to stress again that this isn't really forecasting, or at least I wouldn't rely on it for anything important!

Since I have put an additional region column, we also need to filter on that. <a href="https://datascienceparichay.com/article/pandas-filter-dataframe-for-multiple-conditions/">Read about filtering with pandas</a>.
The basic idea is that you count up all days in the past which had rain above a certain limit and divide by the total number of days. From one forum (<a href="https://cumulus.hosiene.co.uk/viewtopic.php?t=3474">here</a> and <a href="https://cumulus.hosiene.co.uk/viewtopic.php?t=6441">here</a>) it looks like about 1-2mm rain across a day would likely not get in anybody's way, so I have used that as the threshold rather than simply 0mm which is probably a bit too strict.

```python
LIGHT_RAIN_LIMIT = 1.5
df4['count_rain'] = melted[(melted['region']=='SEEP') &amp;amp;amp;amp; (melted['rainfall']&amp;amp;amp;gt;LIGHT_RAIN_LIMIT)].groupby(['month', 'day'])['rainfall'].count().reset_index()['rainfall']
df4['count_not_rain'] = melted[(melted['region']=='SEEP') &amp;amp;amp;amp; (melted['rainfall']&amp;amp;amp;lt;=LIGHT_RAIN_LIMIT)].groupby(['month', 'day'])['rainfall'].count().reset_index()['rainfall']
df4['chance_rain'] = df4['count_rain'] / (df4['count_rain'] + df4['count_not_rain'])
df4['chance_rain'].plot(ylim=0,title="Chance of More Than 1.5mm Rain", xlabel="Day", ylabel="Chance of Rain")
```

| ![UK Rainfall Data - chance of rain]({{site.url}}/assets/2021/06/ChanceOfRain.png) |
|:--:|
| *UK Rainfall Data - chance of rain* |

<h2>Other Sources of UK Rainfall Data</h2>
You may also be interested in other UK Rainfall data such as the <a href="https://catalogue.ceda.ac.uk/uuid/4dc8450d889a491ebb20e724debe2dfb">CEDA </a>archive and the <a href="https://www.metoffice.gov.uk/weather/learn-about/weather/types-of-weather/rain/how-much-does-it-rain-in-the-uk">Met Office</a>.
