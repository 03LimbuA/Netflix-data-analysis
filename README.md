# Netflix-data-analysis

This data analysis project, inspired by and following the tutorial of Youtube Channel [Data Analytics](https://www.youtube.com/@data_analytics69), examines a tabular dataset that encompasses listings of all movies and TV shows available on Netflix, including key details such as cast, ratings, directors, and duration. The official dataset is sourced from [Kaggle Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows). 

For this project, I used Google Colab, leveraging its Jupyter Notebook interface to write and execute Python code. This setup allowed me to analyse the data interactively and visualise the results from the analysis. The complete Google Colab notebook, displaying the coding and resulting data visualisations, can be accessed [here](https://github.com/03LimbuA/Netflix-data-analysis/blob/main/Copy_of_netfllixDATAofficial.ipynb).

## The Process

- Since we’re using python, we import some essential libraries (numpy for numerical operations, pandas for data manipulation, matplotlib for creating visualisations) 
- These libraries provide us with the tools to explore and visualise the dataset
- We use pandas to read the data from the CSV file provided by Kaggle, through the ‘read_csv()’ function 
- An essential part of this analysis report: ‘df.head()’, a function provided by pandas, allows us to see the first few rows of our dataset (useful for quickly inspecting the data we’re working with)
- 'df.info()' gives us details, such as the no. of non-NULL entries, data types, columns - information which is crucial for data processing and ensuring that the data is in the right format for analysis
<img src="https://github.com/user-attachments/assets/9837f16d-c305-4c33-ab57-4d9840a33ebc" width="280" height="200">

- 'df["release_year"].unique()' gives us a list of the distinct years in which the content in our data set was released
<img src="https://github.com/user-attachments/assets/0956595e-076a-4be2-8a7d-55fe65528360" width="400" height="100">

- 'df["type"].unique()' shows us the distinct content types in our data set; we get back 2 distinct types - TV Shows and Movies
- with a pie chart, we can display the 2 different content types, and how much of the data is attributed to each content type:
<img src="https://github.com/user-attachments/assets/5906ac01-55db-44bb-a668-3865c40455a5" width="280" height="200">

- next, we examine the no. of data entries for each release year (below image doesn't display all the rows outputted) 
<img src="https://github.com/user-attachments/assets/0a66a6a0-e60d-448e-9ad8-002c13a0a83d" width="80" height="100">

- we create a bar chart to showcase the top 10 countries which produce the most content on Netflix
<img src="https://github.com/user-attachments/assets/a62d0435-f712-47b2-a771-6332d412e7fa" width="350" height="250">

- we examine the top 20 most common durations for Netflix **Movies** (the data is displayed in ascending order) - the image below doesn't display all the rows outputted
<img src="https://github.com/user-attachments/assets/9d0da5e1-a8b8-4af0-b1e5-2589ecbefbe0" width="80" height="100">

- next, we visually display the information, above, through an area chart
<img src="https://github.com/user-attachments/assets/5f2fc80b-ad0a-49b1-8b67-ddb6d1aca514" width="350" height="250">

- This time, for **TV Shows**, we examine the top 20 most common durations (the data is displayed in ascending order) - the image below doesn't display all the rows outputted
<img src="https://github.com/user-attachments/assets/32943574-aef3-4e41-a527-d3482aab7be1" width="80" height="100">

- Again, we visually display the information, above, through a bar chart
<img src="https://github.com/user-attachments/assets/80713d1a-6ab5-4677-a21e-f5482258892e" width="350" height="250">

- Next, we'll look at the top 20 directors with the most content on Netflix - the image below doesn't display all the rows outputted
<img src="https://github.com/user-attachments/assets/6b3bb368-84cc-4d1f-b27b-06c8581874f3" width="200" height="170">

- We visualise this information, to gain a better understanding of the directors' contributions to Netflix 
<img src="https://github.com/user-attachments/assets/8617a5b1-7c4f-49e1-8a69-4735ddeb1dd3" width="350" height="250">

- Next, we'll look at the unique content categories (aka genre/theme) in our Netflix data set - we find that there are 42 different categories (the image below doesn't display all the rows outputted)
<img src="https://github.com/user-attachments/assets/ea0c2800-7017-400d-be8e-40b1878c60d8" width="170" height="130">

- We, then, display the top 20 most-occurring categories in our dataset (image below doesn't display all the rows outputted)
<img src="https://github.com/user-attachments/assets/4b21cd80-cce8-4eae-9df9-c96dfe5a2ad0" width="260" height="150">

- Next, we'll look at how many times each category appears in our dataset, allowing us to see which content categories are the most and least common on Netflix
<img src="https://github.com/user-attachments/assets/cb89d9c4-921c-489a-a60f-213624f776bd" width="260" height="150">

- We visualise this finding through a bar chart
<img src="https://github.com/user-attachments/assets/7f5be62a-42c2-4470-be56-3ad0a3177ded" width="350" height="250">



**The complete Google Colab notebook, displaying the coding and all resulting data visualisations, can be accessed [here](https://github.com/03LimbuA/Netflix-data-analysis/blob/main/Copy_of_netfllixDATAofficial.ipynb).**

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
