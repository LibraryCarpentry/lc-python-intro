---
title: Conditionals
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Correctly write programs that use if and else statements and simple Boolean expressions (without logical operators).
- Trace the execution of unnested conditionals and conditionals inside loops.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can programs do different things for different data?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use `if` statements to control whether or not a block of code is executed.

An `if` statement is a *conditional* statement that controls whether a block of code is executed or not. The syntax of an `if` statement is similar to a `for` statement:
  - The first line opens with `if` and ends with a colon.
  - The body is indented (usually by 4 spaces)

```python
checkouts = 11
if checkouts > 10.0:
    print(checkouts, 'is over the checkout limit.')

checkouts = 8
if checkouts > 10.0:
    print(checkouts, 'is over the checkout limit.')
```

```output
11 is over the checkout limit.
```

## Conditionals are often used inside loops.

There is not much of a point using a conditional when we know the value (as above), but they're useful when we have a collection to process.

```python
checkouts = [3, 5, 12, 22, 0]
for checkout in checkouts:
    if checkout > 10.0:
        print(checkout, 'is over the checkout limit.')
```

```output
12 is over the checkout limit.
22 is over the checkout limit.
```

## Use `else` to execute a block of code when an `if` condition is *not* true.

And `else` statement can be used following `if` to allow us to specify an alternative code block to execute when the `if` *branch* isn't taken.

```python
checkouts = [3, 5, 12, 22, 0]
for checkout in checkouts:
    if checkout > 10.0:
        print('Warning:', checkout, 'is over the checkout limit.')
    else:
        print(checkout, 'is under the limit.')
```

```output
3 is under the limit.
5 is under the limit.
*Warning* 12 is over the checkout limit.
*Warning* 22 is over the checkout limit.
0 is under the limit.
```

## Use `elif` to specify additional tests.

You can use `elif` (short for "else if") to provide several alternative choices, each with its own test. An `elif` statement should always be associated with an `if` statement, and must come before the `else` statement (which is the catch all).

```python
checkouts = [3, 5, 10, 22, 0]
for checkout in checkouts:
    if checkout > 10.0:
        print('Warning:', checkout, 'is over the checkout limit.')
    elif checkout == 10:
        print(checkout, 'is at the exact checkout limit.')
    else:
        print(checkout, 'is under the limit.')
```

```output
3 is under the limit.
5 is under the limit.
10 is at the exact checkout limit.
Warning: 22 is over the checkout limit.
0 is under the limit.
```

Conditions are tested once, in order and are not re-evaluated if values change. Python steps through the branches of the conditional in order, testing each in turn, so the order of your statements matters. 

```python
grade = 85
if grade >= 70:
    print('grade is C')
elif grade >= 80:
    print('grade is B')
elif grade >= 90:
    print('grade is A')
```

```output
grade is C
```

If a value is adjusted inside of a statement which would change the outcome of previous `if` or `elif` statement, those earlier statements won't be evaluated again unless you re-run the code. 

```python
velocity = 15.0
if velocity > 30.0:
    print('moving too fast')
else:
    print('adjusting velocity')
    velocity = velocity + 15.0
```

```output
adjusting velocity
```

You can use conditionals inside of a loop to adjust values as the loop iterates.

```python
checkouts = 15.0
for i in range(5): # execute the loop 5 times
    print(i, ':', checkouts)
    if checkouts >= 30.0:
        print('too many checkouts')
        checkouts = checkouts - 5.0
    else:
        print('too few checkouts')
        checkouts = checkouts + 10.0
print('final checkouts:', checkouts)
```

```output
0 : 15.0
too few checkouts
1 : 25.0
too few checkouts
2 : 35.0
too many checkouts
3 : 30.0
too many checkouts
4 : 25.0
too few checkouts
final checkouts: 35.0
```

:::::::::::::::::::::::::::::::::::::::::  callout

## Compound conditionals using `and` and `or`

Often, you want some combination of things to be true.  You can combine
relations within a conditional using `and` and `or`.  

```python
checkouts = [3, 70, 120]
user_type = ['faculty', 'graduate', 'undergraduate']

for user in user_type:
    print(user)
    for checkout in checkouts:
        if checkout > 100 and user == 'faculty':
            print(checkout, "Over the faculty checkout limit.")
        elif checkout > 50 and user == 'graduate':
            print(checkout, "Over the graduate student checkout limit.")
        elif checkout > 20 and user == 'undergraduate':
            print(checkout, "Over the undergraduate student checkout limit.")
        else:
            print(checkout, "Under the checkout limit.")
    print()

```
```output
faculty
3 Under the checkout limit.
70 Under the checkout limit.
120 Over the faculty checkout limit.

graduate
3 Under the checkout limit.
70 Over the graduate student checkout limit.
120 Over the graduate student checkout limit.

undergraduate
3 Under the checkout limit.
70 Over the undergraduate student checkout limit.
120 Over the undergraduate student checkout limit.
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Tracing Execution

What does this program print?

```
pressure = 71.9
if pressure > 50.0:
    pressure = 25.0
elif pressure <= 50.0:
    pressure = 0.0
print(pressure)
```

{: python}

:::::::::::::::  solution

## Solution

```output
25.0
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Trimming Values

Fill in the blanks so that this program creates a new list
containing zeroes where the original list's values were negative
and ones where the original list's values were positive.

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = ____
for value in original:
    if ____:
        result.append(0)
    else:
        ____
print(result)
```

```output
[0, 1, 1, 1, 0, 1]
```

:::::::::::::::  solution

## Solution

```python
original = [-1.5, 0.2, 0.4, 0.0, -1.3, 0.4]
result = []
for value in original:
   if value < 0:
       result.append(0)
   else:
      result.append(1)
print(result)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Processing Small Files

Modify this program so that it only processes files with fewer than 50 records.

```python
import glob
import pandas
for filename in glob.glob('data/*.csv'):
    contents = pandas.read_csv(filename)
    ____:
        print(filename, len(contents))
```

:::::::::::::::  solution

## Solution

```python
import glob
import pandas
for filename in glob.glob('data/*.csv'):
   contents = pandas.read_csv(filename)
   if len(contents) < 50:
       print(filename, len(contents))
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Initializing

Modify this program so that it finds the largest and smallest values in the list
no matter what the range of values originally is.

What are the advantages and disadvantages of using this method
to find the range of the data?

```python
values = [...some test data...]
smallest, largest = None, None
for v in values:
    if ____:
        smallest, largest = v, v
    ____:
        smallest = min(____, v)
        largest = max(____, v)
print(smallest, largest)
```

:::::::::::::::  solution

## Solution

```python
values = [1, 3, 4, 5, 10]
smallest, largest = None, None
for v in values:
   if largest is None:
       smallest, largest = v, v
   else:
       smallest = min(smallest, v)
       largest = max(largest, v)
print(smallest, largest)
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::::  callout

## Using Functions With Conditionals in Pandas

Functions will often contain conditionals.  Here is a short example that
will indicate which quartile the argument is in based on hand-coded values
for the quartile cut points.

```python
def calculate_life_quartile(exp):
    if exp < 58.41:
        # This observation is in the first quartile
        return 1
    elif exp >= 58.41 and exp < 67.05:
        # This observation is in the second quartile
       return 2
    elif exp >= 67.05 and exp < 71.70:
        # This observation is in the third quartile
       return 3
    elif exp >= 71.70:
        # This observation is in the fourth quartile
       return 4
    else:
        # This observation has bad data
       return None

calculate_life_quartile(62.5)
```

```output
2
```

That function would typically be used within a `for` loop, but Pandas has
a different, more efficient way of doing the same thing, and that is by
*applying* a function to a dataframe or a portion of a dataframe.  Here
is an example, using the definition above.

```python
data = pd.read_csv('Americas-data.csv')
data['life_qrtl'] = data['lifeExp'].apply(calculate_life_quartile)
```

There is a lot in that second line, so let's take it piece by piece.
On the right side of the `=` we start with `data['lifeExp']`, which is the
column in the dataframe called `data` labeled `lifExp`.  We use the
`apply()` to do what it says, apply the `calculate_life_quartile` to the
value of this column for every row in the dataframe.


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use `if` statements to control whether or not a block of code is executed.
- Conditionals are often used inside loops.
- Use `else` to execute a block of code when an `if` condition is *not* true.
- Use `elif` to specify additional tests.
- Conditions are tested once, in order.
- Create a table showing variables' values to trace a program's execution.

::::::::::::::::::::::::::::::::::::::::::::::::::


