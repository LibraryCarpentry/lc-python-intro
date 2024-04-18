---
title: Libraries & Pandas
teaching: 20
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain what Python libraries and modules are.
- Write Python code that imports and uses modules from Python's standard library.
- Find and read documentation for standard libraries.
- Import the pandas library.
- Use pandas to load a CSV file as a data set.
- Get some basic information about a pandas DataFrame.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I extend the capabilities of Python?
- How can I use Python code that other people have written?
- How can I read tabular data?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Python libraries are powerful collections of tools.

A *Python library* is a collection of files (called *modules*) that contains functions that you can use in your programs. Some libraries (also referred to as packages) contain standard data values or language resources that you can reference in your code. So far, we have used the Python [standard library][stdlib], which is an extensive suite of built-in modules. You can find additional libraries from [PyPI][pypi] (the Python Package Index), though you'll often find references to useful libraries as you're reading tutorials or trying to solve specific programming problems. Some popular libraries for working with data in library fields are:

- [Pandas](https://pandas.pydata.org/) - tabular data analysis tool.
- [Pymarc](https://pypi.org/project/pymarc/) - for working with bibliographic data encoded in MARC21.
- [Matplotlib](https://matplotlib.org/) - data visualization tools.
- [BeautifulSoup](https://pypi.org/project/beautifulsoup4/) - for parsing HTML and XML documents.
- [Requests](https://pypi.org/project/requests/) - for making HTTP requests (e.g., for web scraping, using APIs)
- [Scikit-learn](https://scikit-learn.org/stable/) - machine learning tools for predictive data analysis.
- [NumPy](https://numpy.org/) - numerical computing tools such as mathematical functions and random number generators.


## You must import a library or module before using it.

Use `import` to load a library into a program's memory. Then you can refer to things from the library as `library_name.function`. Let's import and use the `string` library to generate a list of lowercase ASCII letters and to change the case of a text string:


```python
import string

print(f'The lower ascii letters are {string.ascii_lowercase}')
print(string.capwords('capitalise this sentence please.'))
```

```output
The lower ascii letters are abcdefghijklmnopqrstuvwxyz
Capitalise This Sentence Please.
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Dot notation
We introduced Python dot notation when we looked at methods like `list_name.append()`. We can use the same syntax when we call functions of a specific Python library, such as `string.capwords()`. In fact, this dot notation is common in Python, and can refer to relationships between different types of Python objects. Remember that it is always the case that the object to the right of the dot is a part of the larger object to the left. If we expressed capitals of countries using this syntax, for example, we would say, `Brazil.São_Paulo()` or `Japan.Tokyo()`.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use `help` to learn about the contents of a library module.

The `help()` function can tell us more about a module in a library, including more information about its functions and/or variables.

```python
help(string)
```

```output
Help on module string:

NAME
    string - A collection of string constants.

MODULE REFERENCE
    https://docs.python.org/3.6/library/string
    
    The following documentation is automatically generated from the Python
    source files.  It may be incomplete, incorrect or include features that
    are considered implementation detail and may vary between Python
    implementations.  When in doubt, consult the module reference at the
    location listed above.

DESCRIPTION
    Public module variables:
    
    whitespace -- a string containing all ASCII whitespace
    ascii_lowercase -- a string containing all ASCII lowercase letters
    ascii_uppercase -- a string containing all ASCII uppercase letters
    ascii_letters -- a string containing all ASCII letters
    digits -- a string containing all ASCII decimal digits
    hexdigits -- a string containing all ASCII hexadecimal digits
    octdigits -- a string containing all ASCII octal digits
    punctuation -- a string containing all ASCII punctuation characters
    printable -- a string containing all ASCII characters considered printable

CLASSES
    builtins.object
        Formatter
        Template
⋮ ⋮ ⋮
```

## Import specific items

You can use `from ... import ...` to load specific items from a library module to save space. This also helps you write briefer code since you can refer to them directly without using the library name as a prefix everytime.

```python
from string import ascii_letters

print(f'The ASCII letters are {ascii_letters}')
```

```output
The ASCII letters are abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
```
:::::::::::::::::::::::::::::::::::::::::  callout

## Module not found error

Before you can import a Python library, you sometimes will need to download and install it on your machine. Anaconda comes with many of the most popular Python libraries for scientific computing applications built-in, so if you installed Anaconda for this workshop, you'll be able to import many common libraries directly. Some less common tools, like the PyMarc library, however, would need to be installed first.

```python
import pymarc
```

```error
ModuleNotFoundError: No module named 'pymarc'
```

You can find out how to install the library by looking at the documentation. [PyMarc](https://pypi.org/project/pymarc/), for example, recommends using a command line tool, `pip`, to install it. You can install with pip in a Jupyter notebook by starting the command with a percentage symbol, which allows you to run shell commands from Jupyter:

```python
%pip install pymarc
import pymarc
```

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use library aliases

You can use `import ... as ...` to give a library a short *alias* while importing it. This helps you refer to items more efficiently. 

```python
import pandas as pd
```

Many popular libraries have common aliases. For example:

- ```import pandas as pd```
- ```import numpy as np```
- ```import matplotlib as plt```

Using these common aliases can make it easier to work with existing documentation and tutorials. 

## Pandas
`Pandas` is a widely-used Python library for statistics using tabular data.
Essentially, it gives you access to 2-dimensional tables whose columns have names and can have different data types. We can start using pandas by reading a `Comma Separated Values` (CSV) data file with the function `pd.read_csv()`. The function `.read_csv()` expects as an argument the path to and name of the file to be read. This returns a dataframe that you can assign to a variable.

### Find your CSV files

From the file browser in the left sidebar you can select the `data` folder to view the contents of the folder. If you downloaded and uncompressed the dataset correctly, you should see a series of CSV files from 2011 to 2022. If you double-click on the first file, `2011_circ.csv`, you will see a preview of the CSV file in a new tab in the main panel of JupyterLab. 

Let's load that file into a pandas DataFrame, and save it to a new variable called `df`.

```python
df = pd.read_csv('data/2011_circ.csv')
print(df)
```

```output
                       branch                  address     city  zip code  \
0                 Albany Park     5150 N. Kimball Ave.  Chicago   60625.0   
1                     Altgeld    13281 S. Corliss Ave.  Chicago   60827.0   
2              Archer Heights      5055 S. Archer Ave.  Chicago   60632.0   
3                      Austin        5615 W. Race Ave.  Chicago   60644.0   
4               Austin-Irving  6100 W. Irving Park Rd.  Chicago   60634.0   
..                        ...                      ...      ...       ...   
78           Woodson Regional      9525 S. Halsted St.  Chicago   60628.0   
79         Wrightwood-Ashburn      8530 S. Kedzie Ave.  Chicago   60652.0   
80          Renewals - Online                      NaN      NaN       NaN   
81  Talking Books and Braille                      NaN      NaN       NaN   
82         Downloadable Media                      NaN      NaN       NaN   

```
:::::::::::::::::::::::::::::::::::::::::  callout

## File Not Found

Our lessons store their data files in a `data` sub-directory,
which is why the path to the file is `data/2011_circ.csv`.
If you forget to include `data/`, or if you include it but your copy of the file is somewhere else in relation to your Jupyter Notebook, you will get an error that ends with a line like this:

```error
FileNotFoundError: [Errno 2] No such file or directory: 'data/2011_circ.csv'
```

::::::::::::::::::::::::::::::::::::::::::::::::::

`df` is a common variable name that you'll encounter in pandas tutorials online, but in practice it's often better to use more meaningful variable names. Since we have twelve different CSVs to work with, for example, we might want to add the year to the variable name to differentiate between the datasets.

Also, as seen above, the output when you print a dataframe in Jupyter isn't very easy to read. We can use `.head()` to look at just the first few rows in our dataframe formatted in a more convenient way for our Notebook.

```python
df_2011 = pd.read_csv('data/2011_circ.csv')
df_2011.head()
```

## Use the `DataFrame.info()` method to find out more about a dataframe.

```python
df_2011.info()
```

```output
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 83 entries, 0 to 82
Data columns (total 18 columns):
 #   Column     Non-Null Count  Dtype  
---  ------     --------------  -----  
 0   branch     83 non-null     object 
 1   address    80 non-null     object 
 2   city       80 non-null     object 
 3   zip code   80 non-null     float64
 4   january    83 non-null     int64  
 5   february   83 non-null     int64  
 6   march      83 non-null     int64  
 7   april      83 non-null     int64  
 8   may        83 non-null     int64  
 9   june       83 non-null     int64  
 10  july       83 non-null     int64  
 11  august     83 non-null     int64  
 12  september  83 non-null     int64  
 13  october    83 non-null     int64  
 14  november   83 non-null     int64  
 15  december   83 non-null     int64  
 16  ytd        83 non-null     int64  
 17  year       83 non-null     int64  
dtypes: float64(1), int64(14), object(3)
memory usage: 11.8+ KB
```

The `info()` method tells us
- we have a RangeIndex of 83, which means we have 83 rows.
- there are 18 columns, with datatypes of
  - objects (3 columns)
  - 64-bit floating point number (1 column)
  - 64-bit integers (14 columns).
- the dataframe uses 11.8 kilobytes of memory.

## The `DataFrame.columns` variable stores info about the dataframe's columns.

Note that this is data, *not* a method, so do not use `()` to try to call it. It helpfully gives us a list of all of the column names.

```python
print(df_2011.columns)
```

```output
Index(['branch', 'address', 'city', 'zip code', 'january', 'february', 'march',
       'april', 'may', 'june', 'july', 'august', 'september', 'october',
       'november', 'december', 'ytd', 'year'],
      dtype='object')
```

## Use `DataFrame.describe()` to get summary statistics about data.

`DataFrame.describe()` gets the summary statistics of only the columns that have numerical data. All other columns are ignored, unless you use the argument `include='all'`.

```python
df_2011.describe()
```

This gives us, for example, the count, minimum, maximum, and mean values from each numeric column. In the case of the `zip code` column, this isn't helpful, but for the usage data for each month, it's a quick way to scan the range of data over the course of the year.

:::::::::::::::::::::::::::::::::::::::  challenge

## Importing With Aliases

1. Fill in the blanks so that the program below prints `0123456789`.
2. Rewrite the program so that it uses `import` *without* `as`.
3. Which form do you find easier to read?

```python
import string as s
numbers = ____.digits
print(____)
```

:::::::::::::::  solution

## Solution

```python
import string as s
numbers = s.digits
print(numbers)
```

can be written as

```python
import string
numbers = string.digits
print(numbers)
```

Since you just wrote the code and are familiar with it, you might actually
find the first version easier to read. But when trying to read a huge piece
of code written by someone else, or when getting back to your own huge piece
of code after several months, non-abbreviated names are often easier, expect
where there are clear abbreviation conventions.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Locating the Right Module

Given the variables `year`, `month` and `day`, how would you generate a date in the standard iso format:

```python
year = 1971
month = 08
day = 26
```

1. Which [standard library][stdlib] module could help you?
2. Which function would you select from that module?
3. Try to write a program that uses the function.

:::::::::::::::  solution

## Solution

The [datetime module](https://docs.python.org/3/library/datetime.html) seems like it could help you.

You could use `date(year, month, date).isoformat()` to convert your date:

```python
import datetime

iso_date = datetime.date(year, month, day).isoformat()
print(iso_date)
```

or more compactly:

```python
import datetime

print(datetime.date(year, month, day).isoformat())
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

[stdlib]: https://docs.python.org/3/library/
[pypi]: https://pypi.org/

:::::::::: spoiler
### Is there something special about that date in library history?
According to [Washington County Cooperative Library Services](https://www.wccls.org/news/brief-history-library-catalog):
"1971, August 26 – Ohio University’s Alden Library takes computer cataloging online for the first time, building a system where libraries could electronically share catalog records over a network instead of by mailing printed cards or re-entering records in each catalog. That catalog eventually became the core of OCLC WorldCat – a shared online catalog used by libraries in 107 countries and containing 517,963,343 records."
::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Most of the power of a programming language is in its libraries.
- A program must import a library module in order to use it.
- Use `help` to learn about the contents of a library module.
- Import specific items from a library to shorten programs.
- Create an alias for a library when importing it to shorten programs.

::::::::::::::::::::::::::::::::::::::::::::::::::


