---
title: Tidy Data with Pandas
teaching: 90  
exercises: 10  
---

::::::::::::::::::::::::::::::::::::::: objectives
* Identify the characteristics of tidy data and explain its benefits, listing the three principles and discussing how it facilitates data analysis during a review session.
* Use pandas functions like concat(), melt(), and data filtering to manipulate and clean a complex dataset, successfully combining multiple files into a single DataFrame and reshaping it using melt()
::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: questions
- What are the benefits of transforming data into a tidy format for analysis?
- How does the melt() function in pandas facilitate data tidying?
- What are some practical challenges when working with real-world datasets in Python, and how can they be addressed?
::::::::::::::::::::::::::::::::::::::::::::::::::



# Tidy Data in Pandas 

To recap work in the past two episodes, we used the `glob` package to help us work with files on our machine and work on them in Python. We learned about `pandas`, Python's main data cleaning and analysis library.


```python
import glob
import pandas as pd
```

We used `glob` and `pandas` to combine our Chicago public library circulation data into one dataframe. If you have not done this already, the following code will loop through our files, read in the `csv`'s as dataframes, and then append those together in a list and using the pandas `concat` function to merge together. You can check out your Python environment to see if you have a dataframe named `df` by using `%whos`.


```python
%whos
```

    Variable   Type      Data/Info
    ------------------------------
    glob       module    <module 'glob' from '/Use<...>/lib/python3.11/glob.py'>
    pd         module    <module 'pandas' from '/U<...>ages/pandas/__init__.py'>



```python
dfs = [] 

for csv in glob.glob('data/*.csv'):
    data = pd.read_csv(csv)
    dfs.append(data)
```

## Review
1. What is the variable `csv` called in the context of the loop above? 
2. What does `glob.glob('*.csv')` return?
3. What is `*`? 
4. What is this pattern called in programming? 


```python
df = pd.concat(dfs, ignore_index=True)
```

We can look at the head of our combined dataset: 


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1003 entries, 0 to 1002
    Data columns (total 18 columns):
     #   Column     Non-Null Count  Dtype  
    ---  ------     --------------  -----  
     0   branch     1003 non-null   object 
     1   address    643 non-null    object 
     2   city       643 non-null    object 
     3   zip code   643 non-null    float64
     4   january    1003 non-null   int64  
     5   february   1003 non-null   int64  
     6   march      1003 non-null   int64  
     7   april      1003 non-null   int64  
     8   may        1003 non-null   int64  
     9   june       1003 non-null   int64  
     10  july       1003 non-null   int64  
     11  august     1003 non-null   int64  
     12  september  1003 non-null   int64  
     13  october    1003 non-null   int64  
     14  november   1003 non-null   int64  
     15  december   1003 non-null   int64  
     16  ytd        1003 non-null   int64  
     17  year       1003 non-null   int64  
    dtypes: float64(1), int64(14), object(3)
    memory usage: 141.2+ KB



```python
df.tail()
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
      <th>branch</th>
      <th>address</th>
      <th>city</th>
      <th>zip code</th>
      <th>january</th>
      <th>february</th>
      <th>march</th>
      <th>april</th>
      <th>may</th>
      <th>june</th>
      <th>july</th>
      <th>august</th>
      <th>september</th>
      <th>october</th>
      <th>november</th>
      <th>december</th>
      <th>ytd</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>998</th>
      <td>Woodson Regional</td>
      <td>9525 S. Halsted St.</td>
      <td>Chicago</td>
      <td>60628.0</td>
      <td>8074</td>
      <td>7208</td>
      <td>8580</td>
      <td>9424</td>
      <td>8548</td>
      <td>9093</td>
      <td>9747</td>
      <td>9609</td>
      <td>9412</td>
      <td>9631</td>
      <td>8851</td>
      <td>7748</td>
      <td>105925</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>999</th>
      <td>Wrightwood-Ashburn</td>
      <td>8530 S. Kedzie Ave.</td>
      <td>Chicago</td>
      <td>60652.0</td>
      <td>2307</td>
      <td>2496</td>
      <td>2894</td>
      <td>2945</td>
      <td>2915</td>
      <td>3516</td>
      <td>3708</td>
      <td>3303</td>
      <td>3167</td>
      <td>3246</td>
      <td>2873</td>
      <td>2959</td>
      <td>36329</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>1000</th>
      <td>Downloadable Media</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>47023</td>
      <td>41299</td>
      <td>46942</td>
      <td>54642</td>
      <td>55598</td>
      <td>57774</td>
      <td>61783</td>
      <td>63758</td>
      <td>61432</td>
      <td>62406</td>
      <td>66028</td>
      <td>71276</td>
      <td>689961</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>1001</th>
      <td>Renewals - Online</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>209934</td>
      <td>196047</td>
      <td>219824</td>
      <td>213200</td>
      <td>214743</td>
      <td>220111</td>
      <td>245478</td>
      <td>243202</td>
      <td>246715</td>
      <td>258325</td>
      <td>259521</td>
      <td>265531</td>
      <td>2792631</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>1002</th>
      <td>Talking Books and Braille</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>9883</td>
      <td>9978</td>
      <td>9796</td>
      <td>12551</td>
      <td>11076</td>
      <td>11165</td>
      <td>12538</td>
      <td>12080</td>
      <td>11878</td>
      <td>12500</td>
      <td>9959</td>
      <td>10277</td>
      <td>133681</td>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>



Let's take a moment to discuss the setup of our dataframe. It is structured in what is known as a wide format. This format displays an extensive amount of data directly on the screen, with each month's circulation counts spread across the columns in a pivoted manner. This layout makes it easier to read and manually manipulate the data in a spreadsheet and because of this, is often the default output for periodic reporting systems like library circulation systems.

However, this wide format can pose challenges when working with data analysis tools like Pandas. For instance, if we need to identify all the library branches where circulation exceeded 10,000 in any given month, we would have to individually check each column dedicated to a month, which can be quite cumbersome.

This leads us to reshaping our data into a long format. This is sometimes called unpivoting the data, so the month columns become a single varible in the dataset.

## Tidy Data 

Tidy data is a standard way of organizing data values within a dataset, making it easier to work with. Here are the key principles of tidy data:
1. Every column holds a single variable, like "month" or "temperature."
2. Every row represents a single observation, like circulation counts by branch and month.
3. Every cell contains a single value.

The blow visual might help orient us to tidy data. 


![Tidy Data](https://d33wubrfki0l68.cloudfront.net/6f1ddb544fc5c69a2478e444ab8112fb0eea23f8/91adc/images/tidy-1.png)

R for Data Science [12.1](https://r4ds.had.co.nz/tidy-data.html#fig:tidy-structure)

Our current library circulation data is in a pivoted format, where each month is spread out across multiple columns. While this might be visually straightforward to read in a spreadsheet, it's not the best structure for performing more complex tasks like data analysis and visualization in Python.

## Benefits of Tidy Data

Transforming our data into a tidy data format provides several advantages:
- Python tools, such as visualization, filtering, and statistical analysis libraries, work better with data in a tidy format.
- Tidy data makes transforming, summarizing, and visualizing information easier. For instance, comparing monthly trends or calculating annual averages becomes more straightforward.
- As datasets grow, tidy data ensures that they remain manageable and analyses remain accurate.

## Making Our Data Tidy

A good step towards tidying our data would be to consolidate the separate month columns into a column called `month,` and the circulation counts into another column called `circulation_counts.` This adjustment simplifies our dataset and aligns with the principles of tidy data.

To achieve this transformation, we can use a pandas function called `melt()`. This function will help us reshape the data from wide to long format, where each row represents one month's circulation data for a branch, making the dataset tidy and ready for analysis. Let's look at the help for `melt` first.



```python
help(pd.melt)
```

Now, let's tidy our data. We'll create a new dataframe called `df_long` and use `melt` to reshape. `melt` essentially melts down our columns into rows. 


```python
df_long = df.melt(id_vars=['branch', 'address', 'city', 'zip code', 'ytd', 'year'],
                    value_vars=['january', 'february', 'march', 'april', 'may', 'june', 
                                'july', 'august', 'september', 'october', 'november', 'december'],
                    var_name='month', value_name='circulation')

```

In our above code we defined `id_vars` for the columns we do not want to melt. We then identify the columns we do want to melt into rows. `var_name` is the variable name for those columns transformed into rows, e.g. month. `value_names` is the measured varible or in our case `ciruculation`. Let's now look at the new structure of our data.


```python
df_long
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
      <th>branch</th>
      <th>address</th>
      <th>city</th>
      <th>zip code</th>
      <th>ytd</th>
      <th>year</th>
      <th>month</th>
      <th>circulation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Albany Park</td>
      <td>5150 N. Kimball Ave.</td>
      <td>Chicago</td>
      <td>60625.0</td>
      <td>120059</td>
      <td>2011</td>
      <td>january</td>
      <td>8427</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Altgeld</td>
      <td>13281 S. Corliss Ave.</td>
      <td>Chicago</td>
      <td>60827.0</td>
      <td>9611</td>
      <td>2011</td>
      <td>january</td>
      <td>1258</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Archer Heights</td>
      <td>5055 S. Archer Ave.</td>
      <td>Chicago</td>
      <td>60632.0</td>
      <td>101951</td>
      <td>2011</td>
      <td>january</td>
      <td>8104</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Austin</td>
      <td>5615 W. Race Ave.</td>
      <td>Chicago</td>
      <td>60644.0</td>
      <td>25527</td>
      <td>2011</td>
      <td>january</td>
      <td>1755</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Austin-Irving</td>
      <td>6100 W. Irving Park Rd.</td>
      <td>Chicago</td>
      <td>60634.0</td>
      <td>165634</td>
      <td>2011</td>
      <td>january</td>
      <td>12593</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>12031</th>
      <td>Woodson Regional</td>
      <td>9525 S. Halsted St.</td>
      <td>Chicago</td>
      <td>60628.0</td>
      <td>105925</td>
      <td>2014</td>
      <td>december</td>
      <td>7748</td>
    </tr>
    <tr>
      <th>12032</th>
      <td>Wrightwood-Ashburn</td>
      <td>8530 S. Kedzie Ave.</td>
      <td>Chicago</td>
      <td>60652.0</td>
      <td>36329</td>
      <td>2014</td>
      <td>december</td>
      <td>2959</td>
    </tr>
    <tr>
      <th>12033</th>
      <td>Downloadable Media</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>689961</td>
      <td>2014</td>
      <td>december</td>
      <td>71276</td>
    </tr>
    <tr>
      <th>12034</th>
      <td>Renewals - Online</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2792631</td>
      <td>2014</td>
      <td>december</td>
      <td>265531</td>
    </tr>
    <tr>
      <th>12035</th>
      <td>Talking Books and Braille</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>133681</td>
      <td>2014</td>
      <td>december</td>
      <td>10277</td>
    </tr>
  </tbody>
</table>
<p>12036 rows × 8 columns</p>
</div>



For this episode, let's focus on branches and not `Renewals - Online`, `Renewals - Auto`, `Downloadable Media`. We can remove an individual one like so: 


```python
df_long = df_long[df_long['branch'] != 'Downloadable Media']
```

Ok let's look at the branches now: 


```python
df_long['branch'].unique()
```




    array(['Albany Park', 'Altgeld', 'Archer Heights', 'Austin',
           'Austin-Irving', 'Avalon', 'Back of the Yards', 'Beverly',
           'Bezazian', 'Blackstone', 'Brainerd', 'Brighton Park',
           'Bucktown-Wicker Park', 'Budlong Woods', 'Canaryville',
           'Chicago Bee', 'Chicago Lawn', 'Chinatown', 'Clearing', 'Coleman',
           'Daley, Richard J. - Bridgeport', 'Daley, Richard M. - W Humboldt',
           'Douglass', 'Dunning', 'Edgebrook', 'Edgewater', 'Gage Park',
           'Galewood-Mont Clare', 'Garfield Ridge', 'Greater Grand Crossing',
           'Hall', 'Harold Washington Library Center', 'Hegewisch',
           'Humboldt Park', 'Independence', 'Jefferson Park', 'Jeffery Manor',
           'Kelly', 'King', 'Legler Regional', 'Lincoln Belmont',
           'Lincoln Park', 'Little Village', 'Logan Square', 'Lozano',
           'Manning', 'Mayfair', 'McKinley Park', 'Merlo', 'Mount Greenwood',
           'Near North', 'North Austin', 'North Pulaski', 'Northtown',
           'Oriole Park', 'Portage-Cragin', 'Pullman', 'Roden', 'Rogers Park',
           'Roosevelt', 'Scottsdale', 'Sherman Park', 'South Chicago',
           'South Shore', 'Sulzer Regional', 'Thurgood Marshall', 'Toman',
           'Uptown', 'Vodak-East Side', 'Walker', 'Water Works',
           'West Belmont', 'West Chicago Avenue', 'West Englewood',
           'West Lawn', 'West Pullman', 'West Town', 'Whitney M. Young, Jr.',
           'Woodson Regional', 'Wrightwood-Ashburn', 'Renewals - Online',
           'Talking Books and Braille', 'Renewals - Itivia',
           'Renewals - Auto', 'Renewals - Phone', 'Little Italy', 'West Loop'],
          dtype=object)



Whate if we want to remove multiple ones at once? To do this we can introduce a handy function called `isin`. It tests if elements in a list are present in the dataframe. In the below code, this will return `True` when the list element is present in our branch column. We combine this with the `~` operator to negate the expression and remove those rows.


```python
df_long = df_long[~df_long['branch'].isin(["Renewals - Online", "Renewals - Auto", 'Renewals - Itivia',
       'Renewals - Phone', 'Talking Books and Braille'])]
```


```python
df_long
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
      <th>branch</th>
      <th>address</th>
      <th>city</th>
      <th>zip code</th>
      <th>ytd</th>
      <th>year</th>
      <th>month</th>
      <th>circulation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Albany Park</td>
      <td>5150 N. Kimball Ave.</td>
      <td>Chicago</td>
      <td>60625.0</td>
      <td>120059</td>
      <td>2011</td>
      <td>january</td>
      <td>8427</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Altgeld</td>
      <td>13281 S. Corliss Ave.</td>
      <td>Chicago</td>
      <td>60827.0</td>
      <td>9611</td>
      <td>2011</td>
      <td>january</td>
      <td>1258</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Archer Heights</td>
      <td>5055 S. Archer Ave.</td>
      <td>Chicago</td>
      <td>60632.0</td>
      <td>101951</td>
      <td>2011</td>
      <td>january</td>
      <td>8104</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Austin</td>
      <td>5615 W. Race Ave.</td>
      <td>Chicago</td>
      <td>60644.0</td>
      <td>25527</td>
      <td>2011</td>
      <td>january</td>
      <td>1755</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Austin-Irving</td>
      <td>6100 W. Irving Park Rd.</td>
      <td>Chicago</td>
      <td>60634.0</td>
      <td>165634</td>
      <td>2011</td>
      <td>january</td>
      <td>12593</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>12028</th>
      <td>West Pullman</td>
      <td>830 W. 119th St.</td>
      <td>Chicago</td>
      <td>60643.0</td>
      <td>30407</td>
      <td>2014</td>
      <td>december</td>
      <td>2391</td>
    </tr>
    <tr>
      <th>12029</th>
      <td>West Town</td>
      <td>1625 W. Chicago Ave.</td>
      <td>Chicago</td>
      <td>60622.0</td>
      <td>92772</td>
      <td>2014</td>
      <td>december</td>
      <td>6879</td>
    </tr>
    <tr>
      <th>12030</th>
      <td>Whitney M. Young, Jr.</td>
      <td>7901 S. King Dr.</td>
      <td>Chicago</td>
      <td>60619.0</td>
      <td>31993</td>
      <td>2014</td>
      <td>december</td>
      <td>2334</td>
    </tr>
    <tr>
      <th>12031</th>
      <td>Woodson Regional</td>
      <td>9525 S. Halsted St.</td>
      <td>Chicago</td>
      <td>60628.0</td>
      <td>105925</td>
      <td>2014</td>
      <td>december</td>
      <td>7748</td>
    </tr>
    <tr>
      <th>12032</th>
      <td>Wrightwood-Ashburn</td>
      <td>8530 S. Kedzie Ave.</td>
      <td>Chicago</td>
      <td>60652.0</td>
      <td>36329</td>
      <td>2014</td>
      <td>december</td>
      <td>2959</td>
    </tr>
  </tbody>
</table>
<p>11556 rows × 8 columns</p>
</div>




```python
df_long['branch'].unique()
```




    array(['Albany Park', 'Altgeld', 'Archer Heights', 'Austin',
           'Austin-Irving', 'Avalon', 'Back of the Yards', 'Beverly',
           'Bezazian', 'Blackstone', 'Brainerd', 'Brighton Park',
           'Bucktown-Wicker Park', 'Budlong Woods', 'Canaryville',
           'Chicago Bee', 'Chicago Lawn', 'Chinatown', 'Clearing', 'Coleman',
           'Daley, Richard J. - Bridgeport', 'Daley, Richard M. - W Humboldt',
           'Douglass', 'Dunning', 'Edgebrook', 'Edgewater', 'Gage Park',
           'Galewood-Mont Clare', 'Garfield Ridge', 'Greater Grand Crossing',
           'Hall', 'Harold Washington Library Center', 'Hegewisch',
           'Humboldt Park', 'Independence', 'Jefferson Park', 'Jeffery Manor',
           'Kelly', 'King', 'Legler Regional', 'Lincoln Belmont',
           'Lincoln Park', 'Little Village', 'Logan Square', 'Lozano',
           'Manning', 'Mayfair', 'McKinley Park', 'Merlo', 'Mount Greenwood',
           'Near North', 'North Austin', 'North Pulaski', 'Northtown',
           'Oriole Park', 'Portage-Cragin', 'Pullman', 'Roden', 'Rogers Park',
           'Roosevelt', 'Scottsdale', 'Sherman Park', 'South Chicago',
           'South Shore', 'Sulzer Regional', 'Thurgood Marshall', 'Toman',
           'Uptown', 'Vodak-East Side', 'Walker', 'Water Works',
           'West Belmont', 'West Chicago Avenue', 'West Englewood',
           'West Lawn', 'West Pullman', 'West Town', 'Whitney M. Young, Jr.',
           'Woodson Regional', 'Wrightwood-Ashburn', 'Little Italy',
           'West Loop'], dtype=object)



Alright! Now we have the data tidied what can we do with it? What about seeing what branches had over 10,000 circulations counts in any given month.


```python
df_long
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
      <th>branch</th>
      <th>address</th>
      <th>city</th>
      <th>zip code</th>
      <th>ytd</th>
      <th>year</th>
      <th>month</th>
      <th>circulation_count</th>
    </tr>
    <tr>
      <th>date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2011-01-01</th>
      <td>Albany Park</td>
      <td>5150 N. Kimball Ave.</td>
      <td>Chicago</td>
      <td>60625.0</td>
      <td>120059</td>
      <td>2011</td>
      <td>january</td>
      <td>8427</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>Altgeld</td>
      <td>13281 S. Corliss Ave.</td>
      <td>Chicago</td>
      <td>60827.0</td>
      <td>9611</td>
      <td>2011</td>
      <td>january</td>
      <td>1258</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>Archer Heights</td>
      <td>5055 S. Archer Ave.</td>
      <td>Chicago</td>
      <td>60632.0</td>
      <td>101951</td>
      <td>2011</td>
      <td>january</td>
      <td>8104</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>Austin</td>
      <td>5615 W. Race Ave.</td>
      <td>Chicago</td>
      <td>60644.0</td>
      <td>25527</td>
      <td>2011</td>
      <td>january</td>
      <td>1755</td>
    </tr>
    <tr>
      <th>2011-01-01</th>
      <td>Austin-Irving</td>
      <td>6100 W. Irving Park Rd.</td>
      <td>Chicago</td>
      <td>60634.0</td>
      <td>165634</td>
      <td>2011</td>
      <td>january</td>
      <td>12593</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>2014-12-01</th>
      <td>West Pullman</td>
      <td>830 W. 119th St.</td>
      <td>Chicago</td>
      <td>60643.0</td>
      <td>30407</td>
      <td>2014</td>
      <td>december</td>
      <td>2391</td>
    </tr>
    <tr>
      <th>2014-12-01</th>
      <td>West Town</td>
      <td>1625 W. Chicago Ave.</td>
      <td>Chicago</td>
      <td>60622.0</td>
      <td>92772</td>
      <td>2014</td>
      <td>december</td>
      <td>6879</td>
    </tr>
    <tr>
      <th>2014-12-01</th>
      <td>Whitney M. Young, Jr.</td>
      <td>7901 S. King Dr.</td>
      <td>Chicago</td>
      <td>60619.0</td>
      <td>31993</td>
      <td>2014</td>
      <td>december</td>
      <td>2334</td>
    </tr>
    <tr>
      <th>2014-12-01</th>
      <td>Woodson Regional</td>
      <td>9525 S. Halsted St.</td>
      <td>Chicago</td>
      <td>60628.0</td>
      <td>105925</td>
      <td>2014</td>
      <td>december</td>
      <td>7748</td>
    </tr>
    <tr>
      <th>2014-12-01</th>
      <td>Wrightwood-Ashburn</td>
      <td>8530 S. Kedzie Ave.</td>
      <td>Chicago</td>
      <td>60652.0</td>
      <td>36329</td>
      <td>2014</td>
      <td>december</td>
      <td>2959</td>
    </tr>
  </tbody>
</table>
<p>11556 rows × 8 columns</p>
</div>




```python
df_long[df_long['circulation'] > 10000]
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
      <th>branch</th>
      <th>address</th>
      <th>city</th>
      <th>zip code</th>
      <th>ytd</th>
      <th>year</th>
      <th>month</th>
      <th>circulation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>Austin-Irving</td>
      <td>6100 W. Irving Park Rd.</td>
      <td>Chicago</td>
      <td>60634.0</td>
      <td>165634</td>
      <td>2011</td>
      <td>january</td>
      <td>12593</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Bucktown-Wicker Park</td>
      <td>1701 N. Milwaukee Ave.</td>
      <td>Chicago</td>
      <td>60647.0</td>
      <td>173396</td>
      <td>2011</td>
      <td>january</td>
      <td>13113</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Budlong Woods</td>
      <td>5630 N. Lincoln Ave.</td>
      <td>Chicago</td>
      <td>60659.0</td>
      <td>160271</td>
      <td>2011</td>
      <td>january</td>
      <td>12841</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chinatown</td>
      <td>2353 S. Wentworth Ave.</td>
      <td>Chicago</td>
      <td>60616.0</td>
      <td>158449</td>
      <td>2011</td>
      <td>january</td>
      <td>14027</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Edgebrook</td>
      <td>5331 W. Devon Ave.</td>
      <td>Chicago</td>
      <td>60646.0</td>
      <td>129288</td>
      <td>2011</td>
      <td>january</td>
      <td>10231</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>11978</th>
      <td>Edgewater</td>
      <td>1210 W. Elmdale Ave.</td>
      <td>Chicago</td>
      <td>60660.0</td>
      <td>194415</td>
      <td>2014</td>
      <td>december</td>
      <td>15132</td>
    </tr>
    <tr>
      <th>11984</th>
      <td>Harold Washington Library Center</td>
      <td>400 S. State St.</td>
      <td>Chicago</td>
      <td>60605.0</td>
      <td>755189</td>
      <td>2014</td>
      <td>december</td>
      <td>55067</td>
    </tr>
    <tr>
      <th>11993</th>
      <td>Lincoln Belmont</td>
      <td>1659 W. Melrose St.</td>
      <td>Chicago</td>
      <td>60657.0</td>
      <td>164597</td>
      <td>2014</td>
      <td>december</td>
      <td>11857</td>
    </tr>
    <tr>
      <th>12011</th>
      <td>Rogers Park</td>
      <td>6907 N. Clark St.</td>
      <td>Chicago</td>
      <td>60626.0</td>
      <td>136193</td>
      <td>2014</td>
      <td>december</td>
      <td>10293</td>
    </tr>
    <tr>
      <th>12017</th>
      <td>Sulzer Regional</td>
      <td>4455 N. Lincoln Ave.</td>
      <td>Chicago</td>
      <td>60625.0</td>
      <td>490667</td>
      <td>2014</td>
      <td>december</td>
      <td>34266</td>
    </tr>
  </tbody>
</table>
<p>1434 rows × 8 columns</p>
</div>



We can look at specific columns: 


```python
df_long[['branch', 'circulation']]
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
      <th>branch</th>
      <th>circulation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Albany Park</td>
      <td>8427</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Altgeld</td>
      <td>1258</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Archer Heights</td>
      <td>8104</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Austin</td>
      <td>1755</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Austin-Irving</td>
      <td>12593</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>12028</th>
      <td>West Pullman</td>
      <td>2391</td>
    </tr>
    <tr>
      <th>12029</th>
      <td>West Town</td>
      <td>6879</td>
    </tr>
    <tr>
      <th>12030</th>
      <td>Whitney M. Young, Jr.</td>
      <td>2334</td>
    </tr>
    <tr>
      <th>12031</th>
      <td>Woodson Regional</td>
      <td>7748</td>
    </tr>
    <tr>
      <th>12032</th>
      <td>Wrightwood-Ashburn</td>
      <td>2959</td>
    </tr>
  </tbody>
</table>
<p>11556 rows × 2 columns</p>
</div>



We can sort our table: 


```python
df_long.sort_values('circulation', ascending=False)
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
      <th>branch</th>
      <th>address</th>
      <th>city</th>
      <th>zip code</th>
      <th>ytd</th>
      <th>year</th>
      <th>month</th>
      <th>circulation</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2037</th>
      <td>Harold Washington Library Center</td>
      <td>400 S. State St.</td>
      <td>Chicago</td>
      <td>60605.0</td>
      <td>966720</td>
      <td>2011</td>
      <td>march</td>
      <td>89122</td>
    </tr>
    <tr>
      <th>3040</th>
      <td>Harold Washington Library Center</td>
      <td>400 S. State St.</td>
      <td>Chicago</td>
      <td>60605.0</td>
      <td>966720</td>
      <td>2011</td>
      <td>april</td>
      <td>88527</td>
    </tr>
    <tr>
      <th>3541</th>
      <td>Harold Washington Library Center</td>
      <td>400 S. State St.</td>
      <td>Chicago</td>
      <td>60605.0</td>
      <td>937649</td>
      <td>2012</td>
      <td>april</td>
      <td>87689</td>
    </tr>
    <tr>
      <th>7052</th>
      <td>Harold Washington Library Center</td>
      <td>400 S. State St.</td>
      <td>Chicago</td>
      <td>60605.0</td>
      <td>966720</td>
      <td>2011</td>
      <td>august</td>
      <td>85193</td>
    </tr>
    <tr>
      <th>2538</th>
      <td>Harold Washington Library Center</td>
      <td>400 S. State St.</td>
      <td>Chicago</td>
      <td>60605.0</td>
      <td>937649</td>
      <td>2012</td>
      <td>march</td>
      <td>84255</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>10511</th>
      <td>South Shore</td>
      <td>2505 E. 73rd St.</td>
      <td>Chicago</td>
      <td>60649.0</td>
      <td>2571</td>
      <td>2019</td>
      <td>november</td>
      <td>0</td>
    </tr>
    <tr>
      <th>8436</th>
      <td>Whitney M. Young, Jr.</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>4</td>
      <td>2018</td>
      <td>september</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5549</th>
      <td>Humboldt Park</td>
      <td>1605 N. Troy St.</td>
      <td>Chicago</td>
      <td>60647.0</td>
      <td>15947</td>
      <td>2012</td>
      <td>june</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5599</th>
      <td>Albany Park</td>
      <td>5150 N. Kimball Ave.</td>
      <td>Chicago</td>
      <td>60625.0</td>
      <td>572</td>
      <td>2013</td>
      <td>june</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2332</th>
      <td>Galewood-Mont Clare</td>
      <td>6871 W. Belden Ave.</td>
      <td>Chicago</td>
      <td>60707.0</td>
      <td>0</td>
      <td>2022</td>
      <td>march</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>11556 rows × 8 columns</p>
</div>



What if we want to tally up the total circulation for each branch over all years and also see the mean circulation? 


```python
df_long.groupby('branch')['circulation'].agg(total_circulation='sum', mean_circulation='mean')
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
      <th>total_circulation</th>
      <th>mean_circulation</th>
    </tr>
    <tr>
      <th>branch</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Albany Park</th>
      <td>1024714</td>
      <td>7116.069444</td>
    </tr>
    <tr>
      <th>Altgeld</th>
      <td>68358</td>
      <td>474.708333</td>
    </tr>
    <tr>
      <th>Archer Heights</th>
      <td>803014</td>
      <td>5576.486111</td>
    </tr>
    <tr>
      <th>Austin</th>
      <td>200107</td>
      <td>1389.631944</td>
    </tr>
    <tr>
      <th>Austin-Irving</th>
      <td>1359700</td>
      <td>9442.361111</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>West Pullman</th>
      <td>295327</td>
      <td>2050.881944</td>
    </tr>
    <tr>
      <th>West Town</th>
      <td>922876</td>
      <td>6408.861111</td>
    </tr>
    <tr>
      <th>Whitney M. Young, Jr.</th>
      <td>259680</td>
      <td>1803.333333</td>
    </tr>
    <tr>
      <th>Woodson Regional</th>
      <td>823793</td>
      <td>5720.784722</td>
    </tr>
    <tr>
      <th>Wrightwood-Ashburn</th>
      <td>302285</td>
      <td>2099.201389</td>
    </tr>
  </tbody>
</table>
<p>82 rows × 2 columns</p>
</div>



Let's walk through the parts of the code: 
1. `df.groupby('branch')`: This part groups the data by the 'branch' column. That means it organizes the dataframe so that all entries with the same library branch are grouped together. This is similar to the SQL `GROUP BY` statement or the `group_by` function in `dplyr` in R.
2. `['circulation']`: After grouping the data by branch, this specifies that subsequent operations should be performed on the 'circulation' column.
3. `.agg(...)`: The `agg` function is used to apply one or more aggregation operations to the grouped data. Inside the `agg` function:
     - `total_circulation='sum'`: This creates a new column named 'total_circulation' where each entry is the sum of 'circulation' for that branch. It totals up all circulation figures within each branch.
     - `mean_circulation='mean'`: This creates another new column named 'mean_circulation' where each entry is the average 'circulation' for that branch. It calculates the mean circulation figures for each branch.

If we want to group by more than one varible, we add two in a list in the groupby function. 


```python
df_long.groupby(['branch', 'month'])['circulation'].agg(['sum', 'mean'])
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
      <th></th>
      <th>sum</th>
      <th>mean</th>
    </tr>
    <tr>
      <th>branch</th>
      <th>month</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">Albany Park</th>
      <th>april</th>
      <td>79599</td>
      <td>6633.250000</td>
    </tr>
    <tr>
      <th>august</th>
      <td>91416</td>
      <td>7618.000000</td>
    </tr>
    <tr>
      <th>december</th>
      <td>77849</td>
      <td>6487.416667</td>
    </tr>
    <tr>
      <th>february</th>
      <td>76747</td>
      <td>6395.583333</td>
    </tr>
    <tr>
      <th>january</th>
      <td>85952</td>
      <td>7162.666667</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">Wrightwood-Ashburn</th>
      <th>march</th>
      <td>25817</td>
      <td>2151.416667</td>
    </tr>
    <tr>
      <th>may</th>
      <td>22049</td>
      <td>1837.416667</td>
    </tr>
    <tr>
      <th>november</th>
      <td>24124</td>
      <td>2010.333333</td>
    </tr>
    <tr>
      <th>october</th>
      <td>27345</td>
      <td>2278.750000</td>
    </tr>
    <tr>
      <th>september</th>
      <td>25692</td>
      <td>2141.000000</td>
    </tr>
  </tbody>
</table>
<p>984 rows × 2 columns</p>
</div>


:::::::::::::::::::::::::::::::::::::::: keypoints

- In tidy data each variable forms a column, each observation forms a row, and each type of observational unit forms a table.
-  Using pandas for data manipulation to reshape data is fundamental for preparing data for analysis.

::::::::::::::::::::::::::::::::::::::::::::::::::
