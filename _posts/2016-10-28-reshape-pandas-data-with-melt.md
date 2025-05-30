---
layout: post
title: Reshape Pandas Data With Melt
date: 2016-10-28 15:00:50.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- analysis
- data
- data science
- dataframe
- pandas
- python
- reshape
author:
  display_name: deparkes
permalink: "/2016/10/28/reshape-pandas-data-with-melt/"
---
Data tables often come in a format that makes sense to the human who created the table, but that's difficult for analysis. To make analysis easier we can reshape the data into a more computer-friendly form. <a href="https://pandas.pydata.org/">Pandas </a>is a python data analysis library and in this post I reshape pandas data with melt.
<h1>A Reshape Example</h1>
<h2>Simple Dataframe</h2>
Firstly, let's create a simple dataframe in pandas:

```python
data = {'weekday': ["Monday", "Tuesday", "Wednesday",
         "Thursday", "Friday", "Saturday", "Sunday"],
        'Person 1': [12, 6, 5, 8, 11, 6, 4],
        'Person 2': [10, 6, 11, 5, 8, 9, 12],
        'Person 3': [8, 5, 7, 3, 7, 11, 15]}
df = pd.DataFrame(data, columns=['weekday',
        'Person 1', 'Person 2', 'Person 3'])
```

This dataframe is similar to how we might have recorded the data by hand or in a spreadsheet, and could represent test scores of three different people on each day of the week.There is a row for each day of the week, and a separate column for each person:
<table class="dataframe" border="1">
<thead>
<tr>
<th></th>
<th>weekday</th>
<th>Person 1</th>
<th>Person 2</th>
<th>Person 3</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>Monday</td>
<td>12</td>
<td>10</td>
<td>8</td>
</tr>
<tr>
<th>1</th>
<td>Tuesday</td>
<td>6</td>
<td>6</td>
<td>5</td>
</tr>
<tr>
<th>2</th>
<td>Wednesday</td>
<td>5</td>
<td>11</td>
<td>7</td>
</tr>
<tr>
<th>3</th>
<td>Thursday</td>
<td>8</td>
<td>5</td>
<td>3</td>
</tr>
<tr>
<th>4</th>
<td>Friday</td>
<td>11</td>
<td>8</td>
<td>7</td>
</tr>
<tr>
<th>5</th>
<td>Saturday</td>
<td>6</td>
<td>9</td>
<td>11</td>
</tr>
<tr>
<th>6</th>
<td>Sunday</td>
<td>4</td>
<td>12</td>
<td>15</td>
</tr>
</tbody>
</table>
<h2>Fine For Humans - Not So Good For Analysis</h2>
While this simple dataframe structure is fine for a human reader, if we wanted to create  use '<a href="https://pandas.pydata.org/pandas-docs/stable/groupby.html">groupby</a>' operations or begin to <a href="https://en.wikipedia.org/wiki/Database_normalization">normalise</a> this dataframe to we would need to do some reshaping.  We could reshape the dataframe to have a column containing person information, and another column to contain that person's score on a particular day, like this:
<table class="dataframe" border="1">
<thead>
<tr>
<th></th>
<th>weekday</th>
<th>Person</th>
<th>Score</th>
</tr>
</thead>
</table>
<h2>Reshape With Melt</h2>
It is of course possible to reshape a data table by hand, by copying and pasting the values from each person's column into the new 'person' column. This would take a a long time even for this small dataframe, and would be prone to errrors. A much better idea is to reshape the dataframe with <a href="https://pandas.pydata.org/pandas-docs/stable/generated/pandas.melt.html">melt</a>:

```python
melted = pd.melt(df, id_vars=["weekday"],var_name="Person", value_name="Score")
```

Here we have set the variables (columns) that we want to leave unaffected. Variables not included in this list will become rows in a new column (which has the name given by "var_name"). The values belonging to the original rows/columns are found in a new column with a name given by "value_name", and the output dataframe now has three rows for each day of the week - one for each of person 1, 2, and 3. This new form of the dataframe is now more 'normalised' and can have groupby operations applied to it.
<table class="dataframe" border="1">
<thead>
<tr>
<th></th>
<th>weekday</th>
<th>Person</th>
<th>Score</th>
</tr>
</thead>
<tbody>
<tr>
<th>0</th>
<td>Monday</td>
<td>Person 1</td>
<td>12</td>
</tr>
<tr>
<th>1</th>
<td>Tuesday</td>
<td>Person 1</td>
<td>6</td>
</tr>
<tr>
<th>2</th>
<td>Wednesday</td>
<td>Person 1</td>
<td>5</td>
</tr>
<tr>
<th>3</th>
<td>Thursday</td>
<td>Person 1</td>
<td>8</td>
</tr>
<tr>
<th>4</th>
<td>Friday</td>
<td>Person 1</td>
<td>11</td>
</tr>
<tr>
<th>5</th>
<td>Saturday</td>
<td>Person 1</td>
<td>6</td>
</tr>
<tr>
<th>6</th>
<td>Sunday</td>
<td>Person 1</td>
<td>4</td>
</tr>
<tr>
<th>7</th>
<td>Monday</td>
<td>Person 2</td>
<td>10</td>
</tr>
<tr>
<th>8</th>
<td>Tuesday</td>
<td>Person 2</td>
<td>6</td>
</tr>
<tr>
<th>9</th>
<td>Wednesday</td>
<td>Person 2</td>
<td>11</td>
</tr>
<tr>
<th>10</th>
<td>Thursday</td>
<td>Person 2</td>
<td>5</td>
</tr>
<tr>
<th>11</th>
<td>Friday</td>
<td>Person 2</td>
<td>8</td>
</tr>
<tr>
<th>12</th>
<td>Saturday</td>
<td>Person 2</td>
<td>9</td>
</tr>
<tr>
<th>13</th>
<td>Sunday</td>
<td>Person 2</td>
<td>12</td>
</tr>
<tr>
<th>14</th>
<td>Monday</td>
<td>Person 3</td>
<td>8</td>
</tr>
<tr>
<th>15</th>
<td>Tuesday</td>
<td>Person 3</td>
<td>5</td>
</tr>
<tr>
<th>16</th>
<td>Wednesday</td>
<td>Person 3</td>
<td>7</td>
</tr>
<tr>
<th>17</th>
<td>Thursday</td>
<td>Person 3</td>
<td>3</td>
</tr>
<tr>
<th>18</th>
<td>Friday</td>
<td>Person 3</td>
<td>7</td>
</tr>
<tr>
<th>19</th>
<td>Saturday</td>
<td>Person 3</td>
<td>11</td>
</tr>
<tr>
<th>20</th>
<td>Sunday</td>
<td>Person 3</td>
<td>15</td>
</tr>
</tbody>
</table>
<a href="https://stackoverflow.com/questions/28654047/pandas-convert-some-columns-into-rows">Read more about using melt at stackoverflow</a>
