# Netflix-data-analysis

This data analysis project, inspired by and following the tutorial of Youtube Channel 
The dataset source: [Kaggle Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows)

For this data analysis project, I used Google Colab, leveraging its Jupyter Notebook interface to write and execute Python code. This setup allowed me to analyse the data interactively and visualise the results from the analysis.


## The code

```python
import numpy as np
import pandas as pd

import matplotlib.pyplot as plt

df = pd.read_csv("/netflix_titles.csv")
df.head()

df.info()

df.describe(include = "all")

df["release_year"].unique()

df["type"].unique()

colors = [ "red", "purple", "orange" ]
df["type"].value_counts().plot(kind =  "pie", colors = colors)

result = df.groupby("release_year").agg({"type":"count"})
styled_result = result.style.set_table_styles([{"selector": 'td', 'props':[('border', 'ipx solid black')]}])
styled_result

df.isnull().sum()

df.country.value_counts()[:10].plot(kind="bar",color = "pink")

df.rating.value_counts().plot(kind="pie")

df[df["type"]=="Movie"]["duration"].value_counts().sort_values(ascending=False)[:20]

df[df['type']=="Movie"]['duration'].value_counts().sort_values(ascending=False)[:20].plot(kind="area", color='pink')

df[df['type']=="TV Show"]['duration'].value_counts().sort_values(ascending=False)[:20]

df[df['type']=="TV Show"]['duration'].value_counts().sort_values(ascending=False)[:20].plot(kind="bar", color='pink')

df['director'].value_counts().sort_values(ascending=False)[:20]

df['director'].value_counts().sort_values(ascending=False)[:20].plot(kind='bar', color='pink')

list_types = []
for row,items in df.iterrows():
    for item in items['listed_in'].split(','):
        if item.strip() not in list_types:
            list_types.append(item.strip())

list_types,len(list_types)

df['listed_in'].value_counts()[:20]

nums = [0]*len(list_types)
for row,items in df.iterrows():
    for item in items['listed_in'].split(","):
        index = list_types.index(item.strip())
        nums[index]+=1

df_listing = pd.DataFrame({"Type":list_types,"Count":nums})
df_listing.sort_values(by="Count")

df_listing.plot(kind='bar', x='Type', y='Count', color='pink')
