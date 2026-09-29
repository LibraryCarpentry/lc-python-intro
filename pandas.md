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

for csv in sorted(glob.glob('data/*.csv')):
    year = csv[5:9] 
    data = pd.read_csv(csv) 
    data['year'] = year 
    dfs.append(data)

df = pd.concat(dfs, ignore_index=True)

df.head(3)
```
|     | branch         | address               | city    | zip code | january | february | march | april | may  | june  | july  | august | september | october | november | december | ytd    | year |
|-----|----------------|-----------------------|---------|----------|---------|----------|-------|-------|------|-------|-------|--------|-----------|---------|----------|----------|--------|------|
| 0   | Albany Park    | 5150 N. Kimball Ave.  | Chicago | 60625.0  | 8427    | 7023     | 9702  | 9344  | 8865 | 11650 | 11778 | 11306  | 10466     | 10997   | 10567    | 9934     | 120059 | 2011 |
| 1   | Altgeld        | 13281 S. Corliss Ave. | Chicago | 60827.0  | 1258    | 708      | 854   | 804   | 816  | 870   | 713   | 480    | 702       | 927     | 787      | 692      | 9611   | 2011 |
| 2   | Archer Heights | 5055 S. Archer Ave.   | Chicago | 60632.0  | 8104    | 6899     | 9329  | 9124  | 7472 | 8314  | 8116  | 9177   | 9033      | 9709    | 8809     | 7865     | 101951 | 2011 |


### Use `tail()` to look at the end of the DataFrame

We've seen how to look at the first rows in your DataFrame using `.head()`. You can use `.tail()` to look at the final rows. 

```python
df.tail(3)
```
|     | branch        | address              | city    | zip code | january | february | march | april | may  | june | july | august | september | october | november | december | ytd   | year |
|-----|---------------|----------------------|---------|----------|---------|----------|-------|-------|------|------|------|--------|-----------|---------|----------|----------|-------|------|
| 960 | Brighton Park | 4314 S. Archer Ave.  | Chicago | 60632.0  | 1394    | 1321     | 1327  | 1705  | 1609 | 1578 | 1609 | 1512   | 1425      | 1603    | 1579     | 1278     | 17940 | 2022 |
| 961 | South Chicago | 9055 S. Houston Ave. | Chicago | 60617.0  | 496     | 528      | 739   | 775   | 587  | 804  | 720  | 883    | 681       | 697     | 799      | 615      | 8324  | 2022 |
| 962 | Chicago Bee   | 3647 S. State St.    | Chicago | 60609.0  | 799     | 543      | 709   | 803   | 707  | 931  | 778  | 770    | 714       | 835     | 718      | 788      | 9095  | 2022 |


### Slicing a DataFrame

We can use the same slicing syntax that we used for strings and lists to look at a specific range of rows in a DataFrame. 

```python
df[50:60] #look at rows 50 to 59
```
|     | branch         | address                   | city    | zip code | january | february | march | april | may   | june  | july  | august | september | october | november | december | ytd    | year |
|-----|----------------|---------------------------|---------|----------|---------|----------|-------|-------|-------|-------|-------|--------|-----------|---------|----------|----------|--------|------|
| 50  | Near North     | 310 W. Division St.       | Chicago | 60610.0  | 11032   | 10021    | 12911 | 12621 | 12437 | 13988 | 13955 | 14729  | 13989     | 13355   | 13006    | 12194    | 154238 | 2011 |
| 51  | North Austin   | 5724 W. North Ave.        | Chicago | 60639.0  | 2481    | 2045     | 2674  | 2832  | 2202  | 2694  | 3302  | 3225   | 3160      | 3074    | 2796     | 2272     | 32757  | 2011 |
| 52  | North Pulaski  | 4300 W. North Ave.        | Chicago | 60639.0  | 3848    | 3176     | 4111  | 5066  | 3885  | 5105  | 5916  | 5512   | 5349      | 6386    | 5952     | 5372     | 59678  | 2011 |
| 53  | Northtown      | 6435 N. California Ave.   | Chicago | 60645.0  | 10191   | 8314     | 11569 | 11577 | 10902 | 14202 | 15310 | 14152  | 11623     | 12266   | 12673    | 12227    | 145006 | 2011 |
| 54  | Oriole Park    | 7454 W. Balmoral Ave.     | Chicago | 60656.0  | 11999   | 11206    | 13675 | 12755 | 10364 | 12781 | 12219 | 12066  | 10856     | 11324   | 10503    | 9878     | 139626 | 2011 |
| 55  | Portage-Cragin | 5108 W. Belmont Ave.      | Chicago | 60641.0  | 9185    | 7634     | 9760  | 10163 | 7995  | 9735  | 10617 | 11203  | 10188     | 11418   | 10718    | 9517     | 118133 | 2011 |
| 56  | Pullman        | 11001 S. Indiana Ave.     | Chicago | 60628.0  | 1916    | 1206     | 1975  | 2176  | 2019  | 2347  | 2092  | 2426   | 2476      | 2611    | 2530     | 2033     | 25807  | 2011 |
| 57  | Roden          | 6083 N. Northwest Highway | Chicago | 60631.0  | 6336    | 5830     | 7513  | 6978  | 6180  | 8519  | 8985  | 7592   | 6628      | 7113    | 6999     | 6082     | 84755  | 2011 |
| 58  | Rogers Park    | 6907 N. Clark St.         | Chicago | 60626.0  | 10537   | 9683     | 13812 | 13745 | 13368 | 18314 | 20367 | 19773  | 18419     | 18972   | 17255    | 16597    | 190842 | 2011 |
| 59  | Roosevelt      | 1101 W. Taylor St.        | Chicago | 60607.0  | 6357    | 6171     | 8228  | 7683  | 7257  | 8545  | 8134  | 8289   | 7696      | 7598    | 7019     | 6665     | 89642  | 2011 |

### Look at specific columns
To work specifically with one column of a DataFrame we can use a similar syntax, but refer to the name the column of interest. 

```python
df['year'] #look at the year column
```
```output
0      2011
1      2011
2      2011
3      2011
4      2011
       ... 
958    2022
959    2022
960    2022
961    2022
962    2022
Name: year, Length: 963, dtype: object
```

We can add a second square bracket after a column name to refer to specific row indices, either on their own, or using slices to look at ranges.

```python
print(f"first row: {df['year'][0]}") #use double quotes around your fstring if it contains single quotes
print('rows 100 to 102:') #add a new print statement to create a new line
print(df['year'][100:103])
```
```output
first row: 2011
rows 100 to 102:
100    2012
101    2012
102    2012
Name: year, dtype: object
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
0         Albany Park
1             Altgeld
2      Archer Heights
3              Austin
4       Austin-Irving
            ...      
958         Chinatown
959          Brainerd
960     Brighton Park
961     South Chicago
962       Chicago Bee
Name: branch, Length: 963, dtype: object
```

We can use the `.unique()` function to output an array (like a list) of all of the unique values in the `branch` column, and the `.nunique()` function to tell us how many unique values are present.

```python
print(f"Number of unique branches: {df['branch'].nunique()}")
print(df['branch'].unique())
```
```output
Number of unique branches: 82
['Albany Park' 'Altgeld' 'Archer Heights' 'Austin' 'Austin-Irving'
 'Avalon' 'Back of the Yards' 'Beverly' 'Bezazian' 'Blackstone' 'Brainerd'
 'Brighton Park' 'Bucktown-Wicker Park' 'Budlong Woods' 'Canaryville'
 'Chicago Bee' 'Chicago Lawn' 'Chinatown' 'Clearing' 'Coleman'
 'Daley, Richard J. - Bridgeport' 'Daley, Richard M. - W Humboldt'
 'Douglass' 'Dunning' 'Edgebrook' 'Edgewater' 'Gage Park'
 'Galewood-Mont Clare' 'Garfield Ridge' 'Greater Grand Crossing' 'Hall'
 'Harold Washington Library Center' 'Hegewisch' 'Humboldt Park'
 'Independence' 'Jefferson Park' 'Jeffery Manor' 'Kelly' 'King'
 'Legler Regional' 'Lincoln Belmont' 'Lincoln Park' 'Little Village'
 'Logan Square' 'Lozano' 'Manning' 'Mayfair' 'McKinley Park' 'Merlo'
 'Mount Greenwood' 'Near North' 'North Austin' 'North Pulaski' 'Northtown'
 'Oriole Park' 'Portage-Cragin' 'Pullman' 'Roden' 'Rogers Park'
 'Roosevelt' 'Scottsdale' 'Sherman Park' 'South Chicago' 'South Shore'
 'Sulzer Regional' 'Thurgood Marshall' 'Toman' 'Uptown' 'Vodak-East Side'
 'Walker' 'Water Works' 'West Belmont' 'West Chicago Avenue'
 'West Englewood' 'West Lawn' 'West Pullman' 'West Town'
 'Whitney M. Young, Jr.' 'Woodson Regional' 'Wrightwood-Ashburn'
 'Little Italy' 'West Loop']
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
Name: ytd, Length: 82, dtype: int64
```

### Sort pandas series using .sort_values()
The output for code above is another pandas series object. Let's save the output to a new variable so we can then apply the `.sort_values()` method which allows us to view the branches with the *most* usage. The `ascending` parameter for `.sort_values()` takes `True` or `False`. We want to pass `False` so that we sort from the highest values down...

```python
circ_by_branch = df.groupby('branch')['ytd'].sum()
circ_by_branch.sort_values(ascending=False).head(10)
```
```output
branch
Harold Washington Library Center    7498041
Sulzer Regional                     5089225
Lincoln Belmont                     1850964
Edgewater                           1668693
Logan Square                        1539816
Rogers Park                         1515964
Bucktown-Wicker Park                1456669
Lincoln Park                        1441173
Austin-Irving                       1359700
Bezazian                            1357922
Name: ytd, dtype: int64
```
Now we have a list of the branches with the highest number of uses across the whole dataset. 

We can pass multiple columns to `groupby()` to subset the data even further and breakdown the highest usage per year and branch. To do that, we need to pass the column names as a list. We can also chain together many methods into a single line of code. 

```python
circ_by_year_branch = df.groupby(['year', 'branch'])['ytd'].sum().sort_values(ascending=False)
circ_by_year_branch.head(5)
```
```output
year  branch                          
2011  Harold Washington Library Center    966720
2012  Harold Washington Library Center    937649
2013  Harold Washington Library Center    821749
2014  Harold Washington Library Center    755189
2015  Harold Washington Library Center    694528
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
|      |                                  | ytd    |
|------|----------------------------------|--------|
| year | branch                           |        |
| 2011 | Harold Washington Library Center | 966720 |
| 2012 | Harold Washington Library Center | 937649 |
| 2013 | Harold Washington Library Center | 821749 |
| 2014 | Harold Washington Library Center | 755189 |
| 2015 | Harold Washington Library Center | 694528 |
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

Finally, let's save our full concatenated DataFrame to a pickle file that we can use later on in the lesson. We'll save it in the `data/` directory alongside our other data files.

```python
df.to_pickle('data/all_years.pkl')
```


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


