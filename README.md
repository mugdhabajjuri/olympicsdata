# Jimmy Wrangler

This project is a part of course EECS731. In this project we will try to combine two datasets to establish additional value.

This project structure is cloned from [Cookiecutter](https://drivendata.github.io/cookiecutter-data-science/)


Steps followed are :
   - Installing cookiecutter. Run the command 
    
    pip install cookiecutter
   - Then, run the below command from terminal to load the project structure

    cookiecutter https://github.com/drivendata/cookiecutter-data-science

Datasets considered here are **"Olympics data"** and **"World population"**

Path to Olympic data --> /data/external/athlete_events.csv

Path to Population data --> /data/external/population2.csv

Raw data collected from :-

  - athelet_events.csv is taken from [here](https://www.kaggle.com/heesoo37/120-years-of-olympic-history-athletes-and-results#athlete_events.csv) - Kaggle

  - population2.csv is taken from [here](https://en.wikipedia.org/wiki/List_of_countries_by_population_(United_Nations)) - Wikipedia
    
## Data exploration and Basic Hygiene :



```python
import pandas as pd;
import numpy as np;
olympic_data = pd.read_csv('/Users/mugdhabajjuri/DataScience1/data/external/athlete_events.csv')
```


```python
olympic_data.shape
```




    (271116, 15)




```python
olympic_data.head()
```

<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>Height</th>
      <th>Weight</th>
      <th>Team</th>
      <th>NOC</th>
      <th>Games</th>
      <th>Year</th>
      <th>Season</th>
      <th>City</th>
      <th>Sport</th>
      <th>Event</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>1</td>
      <td>A Dijiang</td>
      <td>M</td>
      <td>24.0</td>
      <td>180.0</td>
      <td>80.0</td>
      <td>China</td>
      <td>CHN</td>
      <td>1992 Summer</td>
      <td>1992</td>
      <td>Summer</td>
      <td>Barcelona</td>
      <td>Basketball</td>
      <td>Basketball Men's Basketball</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>1</td>
      <td>2</td>
      <td>A Lamusi</td>
      <td>M</td>
      <td>23.0</td>
      <td>170.0</td>
      <td>60.0</td>
      <td>China</td>
      <td>CHN</td>
      <td>2012 Summer</td>
      <td>2012</td>
      <td>Summer</td>
      <td>London</td>
      <td>Judo</td>
      <td>Judo Men's Extra-Lightweight</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>2</td>
      <td>3</td>
      <td>Gunnar Nielsen Aaby</td>
      <td>M</td>
      <td>24.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Denmark</td>
      <td>DEN</td>
      <td>1920 Summer</td>
      <td>1920</td>
      <td>Summer</td>
      <td>Antwerpen</td>
      <td>Football</td>
      <td>Football Men's Football</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>4</td>
      <td>Edgar Lindenau Aabye</td>
      <td>M</td>
      <td>34.0</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Denmark/Sweden</td>
      <td>DEN</td>
      <td>1900 Summer</td>
      <td>1900</td>
      <td>Summer</td>
      <td>Paris</td>
      <td>Tug-Of-War</td>
      <td>Tug-Of-War Men's Tug-Of-War</td>
      <td>Gold</td>
    </tr>
    <tr>
      <td>4</td>
      <td>5</td>
      <td>Christine Jacoba Aaftink</td>
      <td>F</td>
      <td>21.0</td>
      <td>185.0</td>
      <td>82.0</td>
      <td>Netherlands</td>
      <td>NED</td>
      <td>1988 Winter</td>
      <td>1988</td>
      <td>Winter</td>
      <td>Calgary</td>
      <td>Speed Skating</td>
      <td>Speed Skating Women's 500 metres</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
to_drop = ['ID','Name', 'Height', 'Weight', 'NOC', 'Games', 'Season', 'Event']
olympic_data.drop(to_drop, inplace=True, axis=1)
```


```python
olympic_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sex</th>
      <th>Age</th>
      <th>Team</th>
      <th>Year</th>
      <th>City</th>
      <th>Sport</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>M</td>
      <td>24.0</td>
      <td>China</td>
      <td>1992</td>
      <td>Barcelona</td>
      <td>Basketball</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>1</td>
      <td>M</td>
      <td>23.0</td>
      <td>China</td>
      <td>2012</td>
      <td>London</td>
      <td>Judo</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>2</td>
      <td>M</td>
      <td>24.0</td>
      <td>Denmark</td>
      <td>1920</td>
      <td>Antwerpen</td>
      <td>Football</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>3</td>
      <td>M</td>
      <td>34.0</td>
      <td>Denmark/Sweden</td>
      <td>1900</td>
      <td>Paris</td>
      <td>Tug-Of-War</td>
      <td>Gold</td>
    </tr>
    <tr>
      <td>4</td>
      <td>F</td>
      <td>21.0</td>
      <td>Netherlands</td>
      <td>1988</td>
      <td>Calgary</td>
      <td>Speed Skating</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
olympic_data.dtypes
```




    Sex       object
    Age      float64
    Team      object
    Year       int64
    City      object
    Sport     object
    Medal     object
    dtype: object




```python
df = olympic_data[olympic_data.Year == 2016]
```


```python
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Sex</th>
      <th>Age</th>
      <th>Team</th>
      <th>Year</th>
      <th>City</th>
      <th>Sport</th>
      <th>Medal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>80</td>
      <td>F</td>
      <td>22.0</td>
      <td>Romania</td>
      <td>2016</td>
      <td>Rio de Janeiro</td>
      <td>Weightlifting</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>139</td>
      <td>M</td>
      <td>23.0</td>
      <td>Spain</td>
      <td>2016</td>
      <td>Rio de Janeiro</td>
      <td>Gymnastics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>140</td>
      <td>M</td>
      <td>23.0</td>
      <td>Spain</td>
      <td>2016</td>
      <td>Rio de Janeiro</td>
      <td>Gymnastics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>141</td>
      <td>M</td>
      <td>23.0</td>
      <td>Spain</td>
      <td>2016</td>
      <td>Rio de Janeiro</td>
      <td>Gymnastics</td>
      <td>NaN</td>
    </tr>
    <tr>
      <td>142</td>
      <td>M</td>
      <td>23.0</td>
      <td>Spain</td>
      <td>2016</td>
      <td>Rio de Janeiro</td>
      <td>Gymnastics</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.shape
```




    (13688, 7)




```python
countries = df.groupby('Team')
```


```python
df2 = countries.size().reset_index(name='participants')
```


```python
df2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Team</th>
      <th>participants</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Afghanistan</td>
      <td>3</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Albania</td>
      <td>6</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Algeria</td>
      <td>74</td>
    </tr>
    <tr>
      <td>3</td>
      <td>American Samoa</td>
      <td>4</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Andorra</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.rename(columns={'Team': 'Country'}, inplace=True)
```


```python
df2.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>participants</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Afghanistan</td>
      <td>3</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Albania</td>
      <td>6</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Algeria</td>
      <td>74</td>
    </tr>
    <tr>
      <td>3</td>
      <td>American Samoa</td>
      <td>4</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Andorra</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3 = pd.read_csv('/Users/mugdhabajjuri/DataScience1/data/external/population2.csv')
to_drop = ['Rank', 'UN continentalregion[4]', 'UN statisticalregion[4]', 'Population(1 July 2019)[5]', 'Change']
df3.drop(to_drop, inplace=True, axis=1)
df3.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country or area</th>
      <th>Population(1 July 2018)[5]</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>World</td>
      <td>7,631,091,040</td>
    </tr>
    <tr>
      <td>1</td>
      <td>China</td>
      <td>1,427,647,786</td>
    </tr>
    <tr>
      <td>2</td>
      <td>India</td>
      <td>1,352,642,280</td>
    </tr>
    <tr>
      <td>3</td>
      <td>United States</td>
      <td>327,096,265</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Indonesia</td>
      <td>267,670,543</td>
    </tr>
  </tbody>
</table>
</div>




```python
df3.rename(columns={'Country or area' : 'Country', 'Population(1 July 2018)[5]' : 'Population'}, inplace=True)
```


```python
df3.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>World</td>
      <td>7,631,091,040</td>
    </tr>
    <tr>
      <td>1</td>
      <td>China</td>
      <td>1,427,647,786</td>
    </tr>
    <tr>
      <td>2</td>
      <td>India</td>
      <td>1,352,642,280</td>
    </tr>
    <tr>
      <td>3</td>
      <td>United States</td>
      <td>327,096,265</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Indonesia</td>
      <td>267,670,543</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4 = pd.merge(df2, df3, on=['Country'], how='inner')
```


```python
df4.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>participants</th>
      <th>Population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Afghanistan</td>
      <td>3</td>
      <td>37,171,921</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Albania</td>
      <td>6</td>
      <td>2,882,740</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Algeria</td>
      <td>74</td>
      <td>42,228,408</td>
    </tr>
    <tr>
      <td>3</td>
      <td>American Samoa</td>
      <td>4</td>
      <td>55,465</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Andorra</td>
      <td>4</td>
      <td>77,006</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4.dtypes
```




    Country         object
    participants     int64
    Population      object
    dtype: object




```python
df4["D"] = np.nan
```


```python
df4.dtypes
```




    Country          object
    participants      int64
    Population       object
    D               float64
    dtype: object




```python
df4['Population'] = df4['Population'].str.replace(',','').astype(np.float64)
```


```python
df4.dtypes
```




    Country          object
    participants      int64
    Population      float64
    D               float64
    dtype: object




```python
df4["D"] = (df4['participants'] / df4['Population']) *100
```


```python
df4.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Country</th>
      <th>participants</th>
      <th>Population</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Afghanistan</td>
      <td>3</td>
      <td>37171921.0</td>
      <td>0.000008</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Albania</td>
      <td>6</td>
      <td>2882740.0</td>
      <td>0.000208</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Algeria</td>
      <td>74</td>
      <td>42228408.0</td>
      <td>0.000175</td>
    </tr>
    <tr>
      <td>3</td>
      <td>American Samoa</td>
      <td>4</td>
      <td>55465.0</td>
      <td>0.007212</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Andorra</td>
      <td>4</td>
      <td>77006.0</td>
      <td>0.005194</td>
    </tr>
  </tbody>
</table>
</div>




```python
df4['D'].min()
```




    3.2983350767861355e-06




```python
df4['D'].max()
```




    0.051375727822810816




```python
import plotly.graph_objects as go
fig = go.Figure(data=[go.Pie(labels=df4['Country'], values=df4['participants'], hole=.3)])
fig.show()
```


        <script type="text/javascript">
        window.PlotlyConfig = {MathJaxConfig: 'local'};
        if (window.MathJax) {MathJax.Hub.Config({SVG: {font: "STIX-Web"}});}
        if (typeof require !== 'undefined') {
        require.undef("plotly");
        define('plotly', function(require, exports, module) {
            /**
* plotly.js v1.49.1
* Copyright 2012-2019, Plotly, Inc.
* All rights reserved.
* Licensed under the MIT license
*/


```python
import seaborn as sns
data = pd.read_csv('/Users/mugdhabajjuri/DataScience1/data/external/athlete_events.csv')
data_team=data[data.Team=="United States"]
data_country=data_team.loc[:,["ID","Year"]]

plt.figure(figsize=(20,15))
plt.subplot(211)

country = data_country.groupby("Year")["ID"].nunique().plot(kind = "bar",color = sns.color_palette("husl"))
plt.xticks(rotation = 60)
plt.grid(True,alpha=.3)
plt.xlabel('Olympic Year')
plt.ylabel('Participation rate')
plt.title('Country wise participation rate')
plt.show()

```


![png](output_30_0.png)



```python

```


