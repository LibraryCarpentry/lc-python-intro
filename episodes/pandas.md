---
title: Using Pandas
teaching: 20
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Select specific columns and rows from pandas DataFrames.
- Use pandas methods to calculate sums and means, and to display unique items.
- Sort DataFrame columns (pandas series).
- Save a DataFrame as a CSV or pickle file.


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I work with subsets of data in a pandas DataFrame?
- How can I run summary statistics and sort columns of a DataFrame? 
- How can I save DataFrames to other file formats?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Pinpoint specific rows and columns in a DataFrame

If you don't already have all of the CSV files loaded into a DataFrame, let's do that now: 

```python
import glob
import pandas as pd

dfs = [] 

for csv in glob.glob('data/*.csv'):
    data = pd.read_csv(csv)
    dfs.append(data)

df = pd.concat(dfs, ignore_index=True)
df.head()
```

### Use `tail()` to look at the end of the DataFrame

We've seen how to look at the first rows in your DataFrame using `.head()`. You can use `.tail()` to look at the final rows. You can also pass the number of rows you'd like to view as an argument for `.head()` and `.tail()` in case the the default of five rows doesn't work for you.

```python
df.tail(10)
```

### Slicing a DataFrame

We can use the same slicing syntax that we used for strings and lists to look at a specific range of rows in a DataFrame. 

```python
df[50:60] #look at rows 50 to 59
```

### Look at specific columns
To work specifically with one column of a DataFrame we can use a similar syntax, but refer to the name the column of interest. 

```python
df['year'] #look at the year column
```
```output
0       2011
1       2011
2       2011
3       2011
4       2011
        ... 
998     2014
999     2014
1000    2014
1001    2014
1002    2014
Name: year, Length: 1003, dtype: int64
```

We can add a second square bracket after a column name to refer to specific row indices, either on their own, or using slices to look at ranges.

```python
print(f"first row: {df['year'][0]}") #use double quotes around your fstring if it contains single quotes
print('rows 100 to 102:') #adding a new print statement to create a new line
print(df['year'][100:103])
```
```output
first row: 2011
rows 100 to 102:
100    2016
101    2016
102    2016
Name: year, dtype: int64
```

Columns display differently in our notebook since a column is a different type of object than a full DataFrame. 

```python
type(df['year'])
```
```output
pandas.core.series.Series
```

## Summary statistics on columns
A pandas Series is a one-dimensional array, like a column in a spreadsheet, while a pandas DataFrame is a two-dimensional tabular data structure with labeled axes, similar to a spreadsheet. One of the advantages of pandas is that we can use built-in functions like `max()`, `min()`, `mean()`, and `sum()` to provide summary statistics across Series such as columns. Since it can be difficult to get a sense of the range of data in a large DataFrame by looking over the whole thing manually, these functions can help us understand our dataset quickly and ask specific questions. 

If we wanted to know the range of years covered in this data, for example, we can look at the maximum and minimum values in the `year` column. 

```python
print(f"max year: {df['year'].max()}")
print(f"min year: {df['year'].min()}")
```
```output
max year: 2022
min year: 2011
```

### Summarize columns that hold string objects
We might also want to quickly understand the range of values in columns that contain strings, the `branch` column, for example. We can look at a range of values, but it's hard to tell how many different branches are present in the dataset this way.

```python
df['branch']
```

```output
0                     Albany Park
1                         Altgeld
2                  Archer Heights
3                          Austin
4                   Austin-Irving
                  ...            
998              Woodson Regional
999            Wrightwood-Ashburn
1000           Downloadable Media
1001            Renewals - Online
1002    Talking Books and Braille
Name: branch, Length: 1003, dtype: object
```

We can use the `.unique()` function to output an array (like a list) of all of the unique values in the `branch` column, and the `.nunique()` function to tell us how many unique values are present.

```python
print(f"Number of unique branches: {df['branch'].nunique()}")
print(df['branch'].unique())
```
```output
Number of unique branches: 88
['Albany Park', 'Altgeld', 'Archer Heights', 'Austin',
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
       'Talking Books and Braille', 'Downloadable Media',
       'Renewals - Itivia', 'Renewals - Auto', 'Renewals - Phone',
       'Little Italy', 'West Loop']
```

## Use .groupby() to analyze subsets of data
A reasonable question to ask of the library usage data might be to see which branch library has seen the most checkouts over this ten + year period. We can use `.groupby()` to create subsets of data based on the values in specific columns. For example, let's group our data by branch name, and then look at the `ytd` column to see which branch has the highest usage. `.groupby()` takes a column name as its argument and then for each group we can sum the `ytd` columns using `.sum()`.

```python
df.groupby('branch')['ytd'].sum()
```

```output
branch
Albany Park              1024714
Altgeld                    68358
Archer Heights            803014
Austin                    200107
Austin-Irving            1359700
                          ...   
West Pullman              295327
West Town                 922876
Whitney M. Young, Jr.     259680
Woodson Regional          823793
Wrightwood-Ashburn        302285
Name: ytd, Length: 88, dtype: int64
```

### Sort pandas series using .sort_values()
The output for code above is another pandas series object. Let's save the output to a new variable so we can then apply the `.sort_values()` method which allows us to view the branches with the *most* usage. The `ascending` parameter for `.sort_values()` takes `True` or `False`. We want to pass `False` so that we sort from the highest values down...

```python
circ_by_branch = df.groupby('branch')['ytd'].sum()
circ_by_branch.sort_values(ascending=False).head(10)
```
```output
branch
Renewals - Online                   28441560
Renewals - Auto                     21188737
Downloadable Media                  15709651
Harold Washington Library Center     7498041
Sulzer Regional                      5089225
Lincoln Belmont                      1850964
Edgewater                            1668693
Logan Square                         1539816
Rogers Park                          1515964
Bucktown-Wicker Park                 1456669
Name: ytd, dtype: int64
```
Now we have a list of the branches (including some checkout types) with the highest number of uses across the whole dataset. 

We can pass multiple columns to `groupby()` to subset the data even further and breakdown the highest usage per year and branch. To do that, we need to pass the column names as a list. We can also chain together many methods into a single line of code. 

```python
circ_by_year_branch = df.groupby(['year', 'branch'])['ytd'].sum().sort_values(ascending=False)
circ_by_year_branch.head(5)
```
```output
year  branch           
2020  Renewals - Auto      8222810
2021  Renewals - Auto      6629348
2022  Renewals - Auto      6336579
2019  Renewals - Online    4821180
2018  Renewals - Online    4006963
Name: ytd, dtype: int64
```

## Use .iloc[] and .loc[] to select DataFrame locations.
You can point to specific locations in a DataFrame using two-dimensional numerical indexes with `.iloc[]`.

```python
# print values in the 1st and 2nd to last columns in the first row
# '\n' prints a linebreak
print(f"Branch: {df.iloc[0,0]} \nYTD circ: {df.iloc[0,-2]}")

```

```output
Branch: Albany Park 
YTD circ: 120059
```

`.loc[]` uses the same structure but takes row (index) and column names instead of numerical indexes. Since our `df` rows don't have index names we would still use the default numerical index.

```python
# print the same values as above, using the column names
print(f"Branch: {df.loc[0,'branch']} \nYTD circ: {df.loc[0, 'ytd']}")

```

```output
Branch: Albany Park 
YTD circ: 120059
```

## Save DataFrames

You might want to export the series of usage by year and branch that we just created so that you can share it with colleagues. Pandas includes a variety of methods that begin with `.to_...` that allow us to convert and export data in different ways. First, let's save our series as a DataFrame so we can view the output in a better format in our Jupyter notebook. 

```python
circ_df = circ_by_year_branch.to_frame()
circ_df.head(5)
```

### Save to CSV
Next, let's export the new DataFrame to a CSV file so we can share it with colleagues who love spreadsheets. The `.to_csv()` method expects a string that will be the name of the file as a parameter. Make sure to add the .csv filetype to your file name. 

```python
circ_df.to_csv('high_usage.csv')
```
You should now see, in the JupyterLab file explorer to the left, the new CSV file. If you don't see it, you can hit the refresh icon (it looks like a spinning arrow) above the files pane. You can double-click on the CSV to preview the full spreadsheet in a new Jupyter tab.

::::::::::::::::::::::::::::::::::::::: callout
### Save pickle files
Working with your data in CSVs (especially via tools like Microsoft Excel) can introduce reproducibility issues. For example, you'll sometimes encounter character encoding problems, where certain characters in your dataset will no longer display properly after editing them in a spreadsheet software like Excel, and re-importing them to a pandas DataFrame. 

One way to avoid issues like this is to save Python objects as [pickles](https://docs.python.org/3/library/pickle.html). Technically speaking, the Python pickle module serializes and de-serializes a Python object's structure. In practical terms, pickling allows you to store Python objects (like DataFrames, lists, etc.) efficiently and without losing or corrupting your data. 

You can save a DataFrame to pickle by using the `to_pickle()` method and using the filetype of `pkl`.

```python
circ_df.to_pickle('high_usage.pkl')
```

You can only "see" the data in a pickle file by reloading it into Python. This is a great way to save a DataFrame that you created in one JupyterLab session so that you can reload it later on, or share it with a colleague who's familiar with Python. 

```python
new_df = pd.read_pickle('high_usage.pkl')
new_df.head()
```
:::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Displaying rows and columns

How would you use slicing and column names to select the following subsets of rows and columns from the circulation DataFrame?

1. The city column.
2. Rows 10 to 20.
3. Rows 20 to 30 from the zip code column.

:::::::::::::::  solution

## Solution

```python
#1
df['city']

#2
df[10:21]

#3 
df['zip code'][20:31]

```


:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## Using loc()

How would you use `loc()` to select rows 20 to 30 from the zip code column (the same rows as the last example in the challenge above)?

Tip: slices use "non-inclusive" indexing -- so require you to ask for `df[10:21]` to see row 20, but `loc()` uses inclusive indexing.

:::::::::::::::  solution

## Solution

```python
df.loc[20:30, 'zip code']

```
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Unique items

How would you display:

1. all of the unique zip codes in the dataset?
2. the number of unique zip codes in the dataset?


:::::::::::::::  solution

## Solution

```python

#1
df['zip code'].unique()

#2
df['zip code'].nunique()

```
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Summary statistics and groupby()

We can apply `mean()` to pandas series' in the same way we used `sum()`, `min()`, and `max()` above. How would you display the following? 

1. the mean number of ytd checkouts grouped by zip code?
2. the mean number of ytd checkouts grouped by zip code, and sorted from smallest to largest?


:::::::::::::::  solution

## Solution

```python
#1
df.groupby('zip code')['ytd'].mean()

#2
df.groupby('zip code')['ytd'].mean().sort_values()

```
:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::: keypoints

- Use builtin methods `.sum()`, `.mean()`, `unique()`, and `nunique()` to explore summary statistics on the rows and colums in your DataFrame.
- Use `.groupby()` to work with subsets of your dataset.
- Sort pandas series with `.sort_values()`.
- Use `.loc()` and `.iloc()` to pinpoint specific locations in Pandas DataFrames.
- Save DataFrames to CSV and pickle files using `.to_csv()` and `.to_pickle()`.

::::::::::::::::::::::::::::::::::::::::::::::::::


