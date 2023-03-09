#Project - COVID-19 Analysis [EDA &amp; Visualization]

## DATA UNDERSTANDING

### Importing libraries & data
```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline 
sns.set()
df = pd.read_csv('https://covid.ourworldindata.org/data/owid-covid-data.csv')
df.head()
df.tail()
df.columns
df.shape
df.info()
df.describe()
```
===============================================================================

## EXPLORING WORLD DATA

### Listing all countries / regions in our data
```python
df['location'].unique()
df['location'].nunique()
```
### Selecting the 'World' data
```python
df_world = df[df.location == 'World']
df_world
```
### Finding the date of the maximum number of deaths all over the world
```python
df_world[df_world['new_deaths'] == df_world['new_deaths'].max()]['date']
```
### Creating a summary table for the most recent date all over the world
```python
df_world_recent = df_world[df_world['date'] == df_world.date.max()]
df_world_recent
df_world_recent.groupby("date")[["total_cases","new_cases","new_deaths","total_deaths"]].sum()
```
### Calculating the percentage of confirmed cases regarding the world population
```python
df_world['population'].unique()
df_world['total_cases'].max()
df_world_ratio = df_world['total_cases'].max() / df_world['population'].max()
df_world_ratio
```
===========================================================================================

## VISUALLIZING WORLD DATA
```python
df_world_over_time = df_world.groupby(["date"])[["total_cases","new_cases","total_deaths","new_deaths"]].sum().reset_index().sort_values("date",ascending=True).reset_index(drop=True)
df_world_over_time
```
### Confirmed cases (Total Cases) all over the world

#### Using line-plot
```python
plt.figure(figsize=(20,10))
plt.plot(df_world_over_time.index, df_world_over_time['total_cases'])
plt.title('Evolution of Confirmed Covid-19 cases over time in the word', fontsize=16)
plt.xlabel('Days', fontsize=16)
plt.ylabel('Confirmed cases', fontsize=16)
```
### Total deaths cases evolution over time

##### Using line-plot
```python
plt.figure(figsize=(20,10))
plt.plot(df_world_over_time.index, df_world_over_time['total_deaths'])
plt.title('Evolution of Covid-19 Deaths cases over time in the world', fontsize=16)
plt.xlabel('Days', fontsize=16)
plt.ylabel('Number of Deaths', fontsize=16)
```
### New cases all over the world

#### Using line-plot
```python
plt.figure(figsize=(20,10))
plt.bar(df_world_over_time.index, df_world_over_time['new_cases'])
plt.title('Evolution of Covid-19 New Cases over time in the world', fontsize=16)
plt.xlabel('Days', fontsize=16)
plt.ylabel('New Cases', fontsize=16)
```
### Putting it all together

#### Using line-plot
```python
plt.figure(figsize=(20,10))
plt.plot(df_world_over_time.index, df_world_over_time['total_cases'], label='Confirmed')
plt.plot(df_world_over_time.index, df_world_over_time['total_deaths'], label='Total Deaths')
plt.plot(df_world_over_time.index, df_world_over_time['new_cases'], label='New')
plt.plot(df_world_over_time.index, df_world_over_time['new_deaths'], label='New Deaths')
plt.legend(loc=0)
plt.show()
```





