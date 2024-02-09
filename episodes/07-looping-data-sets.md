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

If you recall from episode 06, the `pd.read_csv()` method takes a text string referencing a filename as an argument. If we have a list of strings that point to our filenames, we can loop through the list to read in each CSV file as a dataframe. Let's print out the maximum values from the 'ytd' (year to date) column for each dataframe.

```python
for filename in ['data/2011_circ.csv', 'data/2012_circ.csv']:
  data = pd.read_csv(filename)
  print(filename, data['ytd'].max())
```

```output
data/2011_circ.csv 9218
data/2012_circ.csv 10010
```

## Use `glob` to find sets of files whose names match a pattern.

Fortunately, we don't have to manually type in a list of all of our filenames. We can use a Python library called `glob`, to work with paths and files in a convenient way. In Unix, the term "globbing" means "matching a set of files with a pattern". Glob gives us some nice pattern matching options:

- `*` will "match zero or more characters"
- `?` will "match exactly one character"

The `glob` library contains a function also called `glob` to match file patterns. For example, `glob.glob('*.txt')` would match all files in the current directory with names that end with `.txt`.

Let's create a list of the usage data CSV files.

```python
import glob
print('all csv files in data directory:', glob.glob('data/*.csv'))
```

```output
all csv files in data directory: ['data/2011_circ.csv', 'data/2016_circ.csv', 'data/2017_circ.csv', 'data/2022_circ.csv', 'data/2018_circ.csv', 'data/2019_circ.csv', 'data/2012_circ.csv', 'data/2013_circ.csv', 'data/2021_circ.csv', 'data/2020_circ.csv', 'data/2015_circ.csv', 'data/2014_circ.csv']
```

## Use `glob` and `for` to process batches of files.

Now we can use glob in a `for` loop to create dataframes from all of the CSV files in the `data` directory. To use tools like `glob` it helps a lot if files are named and stored consistently so that simple patterns will find the right data. You can learn more about how to name files to improve machine-readability from the [Open Science Foundation article on file naming](https://help.osf.io/article/146-file-naming).

```python
for csv in glob.glob('data/*.csv'):
  data = pd.read_csv(csv)
  print(csv, data['ytd'].max())
```

```output
data/2011_circ.csv 1678047
data/2016_circ.csv 3478369
data/2017_circ.csv 3623318
data/2022_circ.csv 6336579
data/2018_circ.csv 4006963
data/2019_circ.csv 4821180
data/2012_circ.csv 1707032
data/2013_circ.csv 2069537
data/2021_circ.csv 6629348
data/2020_circ.csv 8222810
data/2015_circ.csv 3195053
data/2014_circ.csv 2792631
```

The output of the files above may be different for you, depending on what operating system you use. The glob library doesn't have its own internal system for determining how filenames are sorted, but instead relies on the operating system's filesystem. Since operating systems can differ, it is helpful to use Python to manually sort the glob files so that everyone will see the same results, regardless of their operating system. You can do that by applying the Python method `sorted()` to the `glob.glob` list.

```python
for csv in sorted(glob.glob('data/*.csv')):
    data = pd.read_csv(csv)
    print(csv, data['ytd'].max())
```

```output
data/2011_circ.csv 1678047
data/2012_circ.csv 1707032
data/2013_circ.csv 2069537
data/2014_circ.csv 2792631
data/2015_circ.csv 3195053
data/2016_circ.csv 3478369
data/2017_circ.csv 3623318
data/2018_circ.csv 4006963
data/2019_circ.csv 4821180
data/2020_circ.csv 8222810
data/2021_circ.csv 6629348
data/2022_circ.csv 6336579
```

## Appending dataframes to a list

In the example above, we can print out results from each dataframe as we cycle through them, but it would be more convenient if we saved all of the yearly usage data in these CSV files into dataframes that we could work with later on. We can do that by using a list "accumulator" (as we covered in the last episode). 

```python
dfs = [] # this is an empty list to hold all of our dataframes
counter = 1

for csv in sorted(glob.glob('data/*.csv')):
  data = pd.read_csv(csv)
  print(counter, 'Saving', len(data), 'rows from', csv)
  dfs.append(data)
  counter += 1

print('Number of saved dataframes:', len(dfs))
```

```output
1 Saving 83 rows from data/2011_circ.csv
2 Saving 82 rows from data/2012_circ.csv
3 Saving 83 rows from data/2013_circ.csv
4 Saving 83 rows from data/2014_circ.csv
5 Saving 83 rows from data/2015_circ.csv
6 Saving 83 rows from data/2016_circ.csv
7 Saving 83 rows from data/2017_circ.csv
8 Saving 83 rows from data/2018_circ.csv
9 Saving 84 rows from data/2019_circ.csv
10 Saving 85 rows from data/2020_circ.csv
11 Saving 85 rows from data/2021_circ.csv
12 Saving 86 rows from data/2022_circ.csv
Number of saved dataframes: 12
```

## Concatenating dataframes 

There are many different ways to merge, join, and concatenate pandas dataframes together. The [pandas documentation has good examples](https://pandas.pydata.org/docs/user_guide/merging.html) of how to use the `.merge()`, `.join()`, and `.concat()` methods to accomplish different goals. Because all of our CSVs have the exact same columns, if we want to concatenate them vertically (adding all of the rows from each dataframe together in order), we can do so using `concat()`, which takes a list of dataframes as its first argument. Since we aren't using a specific column as a Pandas index, we'll set the argument of `ignore_index` to be True. 

```python
df = pd.concat(dfs, ignore_index=True)
print('Number of rows in df:', len(df))
```

```output
Number of rows in df: 1003
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

## Compile CSVs into one dataframe

Imagine you had a folder named `outputs/` that included all kinds of different file types. Use `glob` and a `for` loop to iterate through all of the CSV files in the folder that have a file name that begins with `data`. Save them to a list called `dfs`, and then use `pd.concat()` to concatenate all of the dataframes from the `dfs` list together into a new dataframe called, `new_df`. You can assume that all of the data CSV files have the same columns so they will concatenate together cleanly using `pd.concat()`.

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

::::::::::::::::::::::::::::::::::::::::::::::::::


