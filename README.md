#Project - COVID-19 Analysis [EDA &amp; Visualization]

## DATA UNDERSTANDING
### Importing libraries & data
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
%matplotlib inline 
sns.set()

df = pd.read_csv('https://covid.ourworldindata.org/data/owid-covid-data.csv')
df.head()
