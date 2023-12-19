---
title: Writing Functions
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain and identify the difference between function definition and function call.
- Write a function that takes a small, fixed number of arguments and produces a single result.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I create my own functions?

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
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(1871, 3, 19)
```

```output
1871/3/19
```

To expand on the recipe metaphor above, the arguments you add to the `()` contain the ingredients for the function, while the body contains the recipe.

Functions with defined parameters will result in an error if they are called without passing an argument:

```python
calc_fine()
```

```error
TypeError                                 Traceback (most recent call last)
Cell In[15], line 1
----> 1 calc_fine()

TypeError: calc_fine() missing 1 required positional argument: 'days_overdue'
```

## Use `return` to pass values back from a function.

In the date example above, we printed the results of the function code to output, but there are better way to handle data and objects created within a function. We can use the keyword `return ...` to send a value back to the "global" environment. (We'll talk more about local and global variables in [episode 11 on function scope](11-scope.md)). A return command can occur anywhere in the function, but is often placed at the very end of a function with the final result. 

```python
def calc_fine(days_overdue):
    if days_overdue <= 10:
        fine =  days_overdue * 0.25
    else:
        fine = (days_overdue * 0.25) + (days_overdue * .50)
    return fine
    
fine = calc_fine(12)
print('Fine owed:', fine)
```

```output
Fine owed: 9.0
```

:::::::::::::::::::::::::::::::::::::::::  callout
### Use f-strings to specify the number of float decimals to display
In the example above, the fine value is displayed as `8.5`, though ideally it would print as `$8.50`. We can use `f-strings` to format specific aspects of strings in Python, such as defining how many decimal points to show. To tell Python the string that follows is an f-string, we simply start it with `f` before the open single (or double) quote. For example: `print(f'This is an f-string')`. But to take advantage of the f-string we should add a `replacement field`, which is an expression delimited by curly braces `{}`. Within the replacement field we can refer to a Python variable and add a `format specifier` of `.2f` to format a float variable to display with two decimal places. Our replacement field, for example, would be `{fine:.2f}`. If you wanted to display a float with three decimal points you would change the format specifier to `{fine:.3f}`.

```python
fine = calc_fine(12)
print(f'Fine owed: ${fine:.2f}')
```
```output
Fine owed: $8.50
```

::::::::::::::::::::::::::::::::::::::::::::::::::

A function that doesn't explicitly `return` a value will automatically return `None`.

```python
result = print_date(1970, 6, 21)
print('result of call is:', result)
```

```output
1970/6/21
result of call is: None
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Definition and Use

What does the following program print?

```python
def report(pressure):
    print('pressure is', pressure)

report(22.5)
```

:::::::::::::::  solution

## Solution

```output
pressure is 22.5
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Order of Operations

The example above:

```python
result = print_date(1871, 3, 19)
print('result of call is:', result)
```

printed:

```output
1871/3/19
result of call is: None
```

Explain why the two lines of output appeared in the order they did.

:::::::::::::::  solution

## Solution

Each line of Python code is executed in order, regardless of whether that line calls
out to a function, which may call out to other functions, or a
variable assignment. In this case, the second line call to `print` will not execute until
the result of `print_date` is complete in the first line.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Encapsulation

Fill in the blanks to create a function that takes a single filename as an argument,
loads the data in the file named by the argument,
and returns the minimum value in that data.

```python
import pandas

def min_in_data(____):
    data = ____
    return ____
```

:::::::::::::::  solution

## Solution

```python
import pandas

def min_in_data(filename):
    data = pandas.read_csv(filename)
    return data.min()
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Find the First

Fill in the blanks to create a function that takes a list of numbers as an argument
and returns the first negative value in the list.
What does your function do if the list is empty?

```python
def first_negative(values):
    for v in ____:
        if ____:
            return ____
```

:::::::::::::::  solution

## Solution

```python
def first_negative(values):
    for v in values:
        if v < 0:
            return v
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Calling by Name

What does this short program print?

```python
def print_date(year, month, day):
    joined = str(year) + '/' + str(month) + '/' + str(day)
    print(joined)

print_date(day=1, month=2, year=2003)
```

1. When have you seen a function call like this before?
2. When and why is it useful to call functions this way?
  {: .python}

:::::::::::::::  solution

## Solution

The program prints:

```output
2003/2/1
```

It is useful to call a function with named arguments to ensure that the
values of each argument are assigned to the intended argument in the
function. This allows the order of arguments to be specified independently
of how they are defined in the function itself.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Encapsulate of If/Print Block

The code below will run on a label-printer for chicken eggs.  A digital scale will report a chicken egg mass (in grams) to the computer and then the computer will print a label.

Please re-write the code so that the if-block is folded into a function.

```python
 import random
 for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass=70+20.0*(2.0*random.random()-1.0)

    print(mass)
   
    #egg sizing machinery prints a label
    if(mass>=85):
       print("jumbo")
    elif(mass>=70):
       print("large")
    elif(mass<70 and mass>=55):
       print("medium")
    else:
       print("small")
```

The simplified program  follows.  What function definition will make it functional?

```python
 # revised version
 import random
 for i in range(10):

    # simulating the mass of a chicken egg
    # the (random) mass will be 70 +/- 20 grams
    mass=70+20.0*(2.0*random.random()-1.0)

    print(mass,print_egg_label(mass))    

```

1. Create a function definition for `print_egg_label()` that will work with the revised program above.  Note, the function's return value will be significant. Sample output might be `71.23 large`.
2. A dirty egg might have a mass of more than 90 grams, and a spoiled or broken egg will probably have a mass that's less than 50 grams.  Modify your `print_egg_label()` function to account for these error conditions. Sample output could be `25 too light, probably spoiled`.

:::::::::::::::  solution

## Solution

```python
def print_egg_label(mass):
  if(mass>=90):
     print(mass, "dirty")
  elif(mass>=85):
     print(mass, "jumbo")
  elif(mass>=70):
     print(mass, "large")
  elif(mass<70 and mass>=55):
     print(mass, "medium")
  else:
     print(mass, "too light, probably spoiled")
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Encapsulating Data Analysis

Assume that the following code has been executed:

```python
import pandas

df = pandas.read_csv('gapminder_gdp_asia.csv', index_col=0)
japan = df.ix['Japan']
```

1. Complete the statements below to obtain the average GDP for Japan
  across the years reported for the 1980s.

```python
year = 1983
gdp_decade = 'gdpPercap_' + str(year // ____)
avg = (japan.ix[gdp_decade + ___] + japan.ix[gdp_decade + ___]) / 2
```

2. Abstract the code above into a single function.

```python
def avg_gdp_in_decade(country, continent, year):
    df = pd.read_csv('gapminder_gdp_'+___+'.csv',delimiter=',',index_col=0)
    ____
    ____
    ____
    return avg
```

3. How would you generalize this function
  if you did not know beforehand which specific years occurred as columns in the data?
  For instance, what if we also had data from years ending in 1 and 9 for each decade?
  (Hint: use the columns to filter out the ones that correspond to the decade,
  instead of enumerating them in the code.)

:::::::::::::::  solution

## Solution

1. 
```python
year = 1983
gdp_decade = 'gdpPercap_' + str(year // 10)
avg = (japan.ix[gdp_decade + '2'] + japan.ix[gdp_decade + '7']) / 2
```

2. 
```python
def avg_gdp_in_decade(country, continent, year):
    df = pd.read_csv('gapminder_gdp_' + continent + '.csv', index_col=0)
    c = df.ix[country]
    gdp_decade = 'gdpPercap_' + str(year // 10)
    avg = (c.ix[gdp_decade + '2'] + c.ix[gdp_decade + '7'])/2
    return avg
```

3. We need to loop over the reported years
  to obtain the average for the relevant ones in the data.

```python
def avg_gdp_in_decade(country, continent, year):
    df = pd.read_csv('gapminder_gdp_' + continent + '.csv', index_col=0)
    c = df.ix[country] 
    gdp_decade = 'gdpPercap_' + str(year // 10)
    total = 0.0
    num_years = 0
    for yr_header in c.index: # c's index contains reported years
        if yr_header.startswith(gdp_decade):
            total = total + c.ix[yr_header]
            num_years = num_years + 1
    return total/num_years
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


