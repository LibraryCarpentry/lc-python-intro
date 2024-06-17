---
title: Looping Over Data Sets
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Be able to read and write globbing expressions that match sets of files.
- Use glob to create lists of files.
- Write for loops to perform operations on files given their names in a list.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I process many data sets with a single command?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use a `for` loop to process files given a list of their names.

If you recall from episode 06, the `pd.read_csv()` method takes a text string referencing a filename as an argument. If we have a list of strings that point to our filenames, we can loop through the list to read in each CSV file as a DataFrame. Let's print out the maximum values from the 'ytd' (year to date) column for each DataFrame.

```python
for filename in ['data/2011_circ.csv', 'data/2012_circ.csv']:
  data = pd.read_csv(filename)
  print(filename, data['ytd'].max())
```

```output
data/2011_circ.csv 966720
data/2012_circ.csv 937649
```

## Use `glob` to find sets of files whose names match a pattern.

Fortunately, we don't have to manually type in a list of all of our filenames. We can use a Python library called `glob`, to work with paths and files in a convenient way. In Unix, the term "globbing" means "matching a set of files with a pattern". Glob gives us some nice pattern matching options:

- `*` will "match zero or more characters"
- `?` will "match exactly one character"

The `glob` library contains a function also called `glob` to match file patterns. For example, `glob.glob('*.txt')` would match all files in the current directory with names that end with `.txt`.

Let's create a list of the usage data CSV files. Because the `.glob()` argument includes a filepath in single quotes, we'll use double quotes around our f-string.

```python
import glob
print(f"all csv files in data directory: {glob.glob('data/*.csv')}")
```

```output
all csv files in data directory: ['data/2011_circ.csv', 'data/2016_circ.csv', 'data/2017_circ.csv', 'data/2022_circ.csv', 'data/2018_circ.csv', 'data/2019_circ.csv', 'data/2012_circ.csv', 'data/2013_circ.csv', 'data/2021_circ.csv', 'data/2020_circ.csv', 'data/2015_circ.csv', 'data/2014_circ.csv']
```

## Use `glob` and `for` to process batches of files.

Now we can use glob in a `for` loop to create DataFrames from all of the CSV files in the `data` directory. To use tools like `glob` it helps if files are named and stored consistently so that simple patterns will find the right data. You can learn more about how to name files to improve machine-readability from the [Open Science Foundation article on file naming](https://help.osf.io/article/146-file-naming).

```python
for csv in glob.glob('data/*.csv'):
  data = pd.read_csv(csv)
  print(csv, data['ytd'].max())
```

```output
data/2011_circ.csv 966720
data/2016_circ.csv 670077
data/2017_circ.csv 634570
data/2022_circ.csv 301340
data/2018_circ.csv 614313
data/2019_circ.csv 581151
data/2012_circ.csv 937649
data/2013_circ.csv 821749
data/2021_circ.csv 271811
data/2020_circ.csv 276878
data/2015_circ.csv 694528
data/2014_circ.csv 755189
```

The output of the files above may be different for you, depending on what operating system you use. The glob library doesn't have its own internal system for determining how filenames are sorted, but instead relies on the operating system's filesystem. Since operating systems can differ, it is helpful to use Python to manually sort the glob files so that everyone will see the same results, regardless of their operating system. You can do that by applying the Python method `sorted()` to the `glob.glob` list.

```python
for csv in sorted(glob.glob('data/*.csv')):
    data = pd.read_csv(csv)
    print(csv, data['ytd'].max())
```

```output
data/2011_circ.csv 966720
data/2012_circ.csv 937649
data/2013_circ.csv 821749
data/2014_circ.csv 755189
data/2015_circ.csv 694528
data/2016_circ.csv 670077
data/2017_circ.csv 634570
data/2018_circ.csv 614313
data/2019_circ.csv 581151
data/2020_circ.csv 276878
data/2021_circ.csv 271811
data/2022_circ.csv 301340
```


## Appending DataFrames to a list

In the example above, we can print out results from each DataFrame as we cycle through them, but it would be more convenient if we saved all of the yearly usage data in these CSV files into DataFrames that we could work with later on. 

### Convert Year in filenames to a column
Before we join the data from each CSV into a single DataFrame, we'll want to make sure we keep track of which year each dataset comes from. To do that we can capture the year from each file name and save it to a new column for all of the rows in each CSV. Let's see how this works by looping through each of our CSVs.

```python
for csv in sorted(glob.glob('data/*.csv')):
        year = csv[5:9] #the 5th to 9th characters in each file match the year
        print(f'filename: {csv} year: {year}')
```

```output
filename: data/2011_circ.csv year: 2011
filename: data/2012_circ.csv year: 2012
filename: data/2013_circ.csv year: 2013
filename: data/2014_circ.csv year: 2014
filename: data/2015_circ.csv year: 2015
filename: data/2016_circ.csv year: 2016
filename: data/2017_circ.csv year: 2017
filename: data/2018_circ.csv year: 2018
filename: data/2019_circ.csv year: 2019
filename: data/2020_circ.csv year: 2020
filename: data/2021_circ.csv year: 2021
filename: data/2022_circ.csv year: 2022
```

Once we've saved the `year` variable from each file name, we can assign it to every row in a column for each CSV by assigning `data['year'] = year` inside of the loop. 

To collect the data from each CSV we'll use a list "accumulator" (as we covered in the last episode) and append each DataFrame to an empty list. You can create an empty list by assigning a variable to empty square brackets before the loop begins.

```python
dfs = [] # an empty list to hold all of our DataFrames
counter = 1

for csv in sorted(glob.glob('data/*.csv')):
  year = csv[5:9] 
  data = pd.read_csv(csv) 
  data['year'] = year 
  print(f'{counter} Saving {len(data)} rows from {csv}')
  dfs.append(data)
  counter += 1

print(f'Number of saved DataFrames: {len(dfs)}')
```

```output
1 Saving 80 rows from data/2011_circ.csv
2 Saving 79 rows from data/2012_circ.csv
3 Saving 80 rows from data/2013_circ.csv
4 Saving 80 rows from data/2014_circ.csv
5 Saving 80 rows from data/2015_circ.csv
6 Saving 80 rows from data/2016_circ.csv
7 Saving 80 rows from data/2017_circ.csv
8 Saving 80 rows from data/2018_circ.csv
9 Saving 81 rows from data/2019_circ.csv
10 Saving 81 rows from data/2020_circ.csv
11 Saving 81 rows from data/2021_circ.csv
12 Saving 81 rows from data/2022_circ.csv
Number of saved DataFrames: 12
```

We can check to make sure the year was properly saved by looking at the first DataFrame in the `dfs` list. If you scroll to the right you should see the first two rows of the `year` column both have the value `2011`.

```python
dfs[0].head(2) # we can add a number to head() to ask for a specific number of rows
```
```output
|     | branch      | address               | city    | zip code | january | february | march | april | may  | june  | july  | august | september | october | november | december | ytd    | year |
|-----|-------------|-----------------------|---------|----------|---------|----------|-------|-------|------|-------|-------|--------|-----------|---------|----------|----------|--------|------|
| 0   | Albany Park | 5150 N. Kimball Ave.  | Chicago | 60625.0  | 8427    | 7023     | 9702  | 9344  | 8865 | 11650 | 11778 | 11306  | 10466     | 10997   | 10567    | 9934     | 120059 | 2011 |
| 1   | Altgeld     | 13281 S. Corliss Ave. | Chicago | 60827.0  | 1258    | 708      | 854   | 804   | 816  | 870   | 713   | 480    | 702       | 927     | 787      | 692      | 9611   | 2011 |

```

## Concatenating DataFrames 

There are many different ways to merge, join, and concatenate pandas DataFrames together. The [pandas documentation has good examples](https://pandas.pydata.org/docs/user_guide/merging.html) of how to use the `.merge()`, `.join()`, and `.concat()` methods to accomplish different goals. Because all of our CSVs have the exact same columns, if we want to concatenate them vertically (adding all of the rows from each DataFrame together in order), we can do so using `concat()`, which takes a list of DataFrames as its first argument. Since we aren't using a specific column as a pandas index, we'll set the argument of `ignore_index` to be True. 

```python
df = pd.concat(dfs, ignore_index=True)
f'Number of rows in df: {len(df)}'
```

```output
'Number of rows in df: 963'
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Determining Matches

Which of these files would be matched by the expression `glob.glob('data/*circ.csv')`?

1. `data/2011_circ.csv`
2. `data/2012_circ_stats.csv`
3. `circ/2013_circ.csv`
4. Both 1 and 3

:::::::::::::::  solution

## Solution

Only item 1 is matched by the wildcard expression `data/*circ.csv`. 

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Minimum circulation per year

Modify the following code to print out the lowest value in the `ytd` column from each year/file.

```python
import pandas as pd
for csv in sorted(glob.glob('data/*.csv')):
    data = pd.read_csv(____)
    print(csv, data['____'].____())
    
```

:::::::::::::::  solution

## Solution

```python
import pandas as pd
for csv in sorted(glob.glob('data/*.csv')):
    data = pd.read_csv(csv)
    print(csv, data['ytd'].min())
    
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Compile CSVs into one DataFrame

Imagine you had a folder named `outputs/` that included all kinds of different file types. Use `glob` and a `for` loop to iterate through all of the CSV files in the folder that have a file name that begins with `data`. Save them to a list called `dfs`, and then use `pd.concat()` to concatenate all of the DataFrames from the `dfs` list together into a new DataFrame called, `new_df`. You can assume that all of the data CSV files have the same columns so they will concatenate together cleanly using `pd.concat()`.

:::::::::::::::  solution

## Solution

```python
import pandas as pd

dfs = []

for csv in sorted(glob.glob('outputs/data*.csv')):
    data = pd.read_csv(csv)
    dfs.append(data)
    
new_df = pd.concat(dfs, ignore_index=True)
    
```

:::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use a `for` loop to process files given a list of their names.
- Use `glob.glob` to find sets of files whose names match a pattern.
- Use `glob` and `for` to process batches of files.
- Use a list “accumulator” to append a DataFrame to an empty list `[]`.
- The `.merge()`, `.join()`, and `.concat()` methods can combine pandas DataFrames.

::::::::::::::::::::::::::::::::::::::::::::::::::


