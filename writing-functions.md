---
title: Writing Functions
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain and identify the difference between function definition and function call.
- Write a function that takes a small, fixed number of arguments and produces a single result.
- Identify local and global variables.


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I create my own functions?
- How do variables inside and outside of functions work?
- How can I make my functions easier to understand?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use functions to make your code easier to understand.

Human beings can only keep a few items in working memory at a time. But we can work with larger and more complicated ideas by breaking content down into pieces. Functions serve a similar purpose in Python. We can create our own functions to *encapsulate* complexity and treat specific actions or ideas as a single "thing". Functions also enable us to *re-use* code so we can write code one time, but use it many times.

## Define a function using `def` with a name, parameters, and a block of code.

Begin each definition of a new function with the keyword `def` (for "define"), followed by the name of the function. Function names follow the same rules as variable names. Next, add your *parameters* in parentheses. You should still use empty parentheses if the function doesn't take any inputs. Finally, like in conditionals and loops, you'll add a colon and an indented block of code that will contain the body of your function.

```python
def print_greeting():
    print('Hello!')
```


## Defining a function does not run it.

Note that we don't have any output when we run code to define a function. This is similar to assigning a value to a variable. The function definition is sort of like a recipe in a cookbook - the recipe doesn't create a meal until we use it. So we need to "call" a function to execute the code it contains. This means that Python won't show you errors in your function until you call it.  So when a definition of a function runs without error it doesn't mean that there won't be errors when it executes later.

```python
print_greeting()
```

```output
Hello!
```

## Arguments in call are matched to parameters in definition.

Functions are highly useful when they use parameters to pull in data. You can specify *parameters* when you define a function which become variables when the function is executed.

```python
def print_date(year, month, day):
    joined = f'{year}/{month}/{day}'
    print(joined)

print_date(1871, 3, 19)
```

```output
1871/3/19
```

To expand on the recipe metaphor above, the arguments you add to the `()` contain the ingredients for the function, while the body contains the recipe.

Functions with defined parameters will result in an error if they are called without passing an argument:

```python
print_date()
```

```error
TypeError                                 Traceback (most recent call last)
Cell In[15], line 1
----> 1 print_date()

TypeError: print_date() missing 3 required positional arguments: 'year', 'month', and 'day'
```

## Use `return` to pass values back from a function.

In the date example above, we printed the results of the function code to output, but there are better way to handle data and objects created within a function. We can use the keyword `return ...` to send a value back to the "global" environment. (We'll learn about local and global variables below). A return command can occur anywhere in the function, but is often placed at the very end of a function with the final result. 

```python
def calc_fine(days_overdue):
    if days_overdue <= 10:
        fine =  days_overdue * 0.25
    else:
        fine = (days_overdue * 0.25) + (days_overdue * .50)
    return fine
    
fine = calc_fine(12)
f'Fine owed: ${fine}'
```

```output
'Fine owed: $9.0'
```

:::::::::::::::::::::::::::::::::::::::::  callout
### Specify the number of float decimals to display
In the example above, the fine value is displayed as `9.0`, though ideally it would print as `$9.00`. We can use the `f-string format specifier` of `.2f` to display two decimal points: `{fine:.2f}`. If you wanted to display a float with three decimal points you would change the format specifier to `{fine:.3f}`. Here's a [cheat sheet of other f-string number formats](https://fstring.help/cheat/).

```python
fine = calc_fine(12)
f'Fine owed: ${fine:.2f}'
```
```output
'Fine owed: $9.00'
```

::::::::::::::::::::::::::::::::::::::::::::::::::

A function that doesn't explicitly `return` a value will automatically return `None`.

```python
result = print_date(1970, 6, 21)
print(f'result of call is: {result}')
```

```output
1970/6/21
result of call is: None
```

## Variable scope

When we define a variable inside of a function in Python, it's known as a `local` variable, which means that it's not visible to -- or known by -- the rest of the program. Variables that we define outside of functions are `global` and are therefore visible throughout the program, *including* from within other functions. The part of a program in which a variable is visible is called its *scope*.

This is helpful for people using or writing functions, because they don't need to worry about repeating variable names that have been created elsewhere in the program. 

```python
initial_fine = 0.25
late_fine = 0.50

def calc_fine(days_overdue):
    if days_overdue <= 10:
        days_overdue =  days_overdue * initial_fine
    else:
        days_overdue = (days_overdue * initial_fine) + (days_overdue * late_fine)
    return days_overdue
    
```

- `initial_fine` and `late_fine` are *global variables*.
- `days_overdue` is a *local variable* in `calc_fine`. Note that a function parameter is a variable that is automatically assigned a value when the function is called and so acts as a local variable.

```python
fine = calc_fine(12)
print(f'Fine owed: ${fine:.2f}')
print(f'Fine rates: ${initial_fine:.2f}, ${late_fine:.2f}')
print(f'Days overdue: {days_overdue}')
```

```output
Fine owed: $9.00
Fine rates: $0.25, $0.50
```

```error
NameError                                 Traceback (most recent call last)
Cell In[22], line 4
      2 print(f'Fine owed: ${fine:.2f}')
      3 print(f'Fine rates: ${initial_fine:.2f}, ${late_fine:.2f}')
----> 4 print(f'Days overdue: {days_overdue}')

NameError: name 'days_overdue' is not defined
```

## Use docstrings to provide online help.

If the first thing in a function is a string that isn’t assigned to a variable, that string is attached to the function as its documentation. This kind of documentation at the beginning of a function is called a `docstring`. 

```python
def fahr_to_celsius(temp):
    "Input a fahrenheit temperature and return the value in celsius"
    return ((temp - 32) * (5/9))
```

This is helpful because we can now ask Python’s built-in help system to show us the documentation for the function:

```python
help(fahr_to_celsius)
```

```output
Help on function fahr_to_celsius in module __main__:

fahr_to_celsius(temp)
    Input a fahrenheit temperature and return the value in celsius
```

We don’t need to use triple quotes when we write a docstring, but if we do, we can break the string across multiple lines:

```python
def fahr_to_celsius(temp):
    """Convert fahrenheit values to celsius
    Input a value in fahrenheit
    Output a value in celsius"""
    return ((temp - 32) * (5/9))
```


:::::::::::::::::::::::::::::::::::::::  challenge

## Create a function

Write a function called `addition` that takes two parameters and returns their sum. After defining the function, call it with several arguments and print out the results. 


:::::::::::::::  solution

## Solution

```python
def addition(x, y):
    return x + y

addition(3, 6)
```

```output
9

```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Conditional statements within functions

Create a function called `grade_converter` that takes a numerical score (0 - 100) as its parameter and returns a letter grade based on the score:

- 90 and above returns 'A'
- 80 to 89 returns 'B'
- 70 to 79 returns 'C'
- 60 to 69 returns 'D'
- Below 60 returns 'F'

After defining the function, test it with a variety of scores to test it out. 

:::::::::::::::  solution

## Solution

```python
def grade_converter(score):
    if score > 100 or score < 0:
        return 'Invalid score'
    elif score >= 90:
        return 'A'
    elif score >= 80:
        return 'B'
    elif score >= 70:
        return 'C'
    elif score >= 60:
        return 'D'
    elif score <= 59:
        return 'F'

grade_converter(88)
```

```output
'B'
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## Local and global variables

List all of the global variables and all of the local variables in the following code. 

```python
fine_rate = 0.25

def fine(days_overdue):
    if days_overdue <= 10:
        fine =  days_overdue * fine_rate
    else:
        fine = (days_overdue * fine_rate) + (days_overdue * (fine_rate*2))
    return fine
    
total_fine = calc_fine(20)
f'Fine owed: ${total_fine:.2f}'

```

```output
'Fine owed: $15.00'
```
:::::::::::::::  solution

## Solution

Global variables:

- fine_rate
- total_fine

Local variables:

- days_overdue
- fine

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## CSVs to Pandas function
In the [Looping Data Sets episode](looping-data-sets.html#appending-dataframes-to-a-list), we learned to use glob to loop through a directory of CSV files and convert them to a Pandas DataFrame. 

Write a function that converts a directory of CSV files into a single Pandas DataFrame. The function should accept one parameter: a string that includes the path and glob wildcard expression to point to a set of CSV files (e.g., `'data/*.csv'`). We can assume, for these purposes, that all of the DataFrames have the same column names so that you can use `pd.concat(dfs, ignore_index=True)` at the end of the function to concatenate a list of DataFrames into a single DataFrame.


:::::::::::::::  solution

## Solution

```python
import glob
import pandas as pd

def concat_csvs(path):
    
    dfs = [] 

    for csv in sorted(glob.glob(path)):
        data = pd.read_csv(csv)
        dfs.append(data)
    
    df = pd.concat(dfs, ignore_index=True)
    return df

df = concat_csvs('data/*.csv')

```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Break programs down into functions to make them easier to understand.
- Define a function using `def` with a name, parameters, and a block of code.
- Defining a function does not run it.
- Arguments in call are matched to parameters in definition.
- Functions may return a result to their caller using `return`.

::::::::::::::::::::::::::::::::::::::::::::::::::


