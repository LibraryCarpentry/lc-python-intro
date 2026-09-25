---
title: Conditionals
teaching: 15
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Correctly write programs that use `if` and `else` statements using Boolean expressions.
- Trace the execution of conditionals inside of loops.

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
    print(f'{checkouts} is over the limit.')

checkouts = 8
if checkouts > 10.0:
    print(f'{checkouts} is over the limit.')
```

```output
11 is over the limit.
```

## Conditionals are often used inside loops.

There is not much of a point using a conditional when we know the value (as above), but they're useful when we have a collection to process.

```python
checkouts = [0, 3, 10, 12, 22]
for checkout in checkouts:
    if checkout > 10.0:
        print(f'{checkout} is over the limit.')
```

```output
12 is over the limit.
22 is over the limit.
```

## Use `else` to execute a block of code when an `if` condition is *not* true.

An `else` statement can be used following `if` to allow us to specify an alternative code block to execute when the `if` *branch* is not taken.

```python
for checkout in checkouts:
    if checkout > 10.0:
        print(f'{checkout} is over the limit.')
    else:
        print(f'{checkout} is under the limit.')
```

```output
0 is under the limit.
3 is under the limit.
10 is under the limit.
12 is over the limit.
22 is over the limit.
```

Notice that our `else` statement led to a false output that says 10 is under the limit. We can address this by adding a different kind of `else` statement.

## Use `elif` to specify additional tests.

You can use `elif` (short for "else if") to provide several alternative choices, each with its own test. An `elif` statement should always be associated with an `if` statement, and must come before the `else` statement (which is the catch all).

```python
for checkout in checkouts:
    if checkout > 10.0:
        print(f'*Warning*: {checkout} is over the limit.')
    elif checkout == 10:
        print(f'{checkout} is at the exact limit.')
    else:
        print(f'{checkout} is under the limit.')
```

```output
0 is under the limit.
3 is under the limit.
10 is at the exact limit.
*Warning*: 12 is over the limit.
*Warning*: 22 is over the limit.

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

## Compound conditionals using `and` and `or`

Often, you want some combination of things to be true.  You can combine
relations within a conditional using `and` and `or`.  

We can also check if something is less/greater than or equal to a value by using `>=` and `<=` operators.

```python
checkouts = [3, 50, 120]
users = ['fac', 'grad']

for user in users:
    for checkout in checkouts:
        #faculty checkout limit is 100
        if checkout >= 100 and user == 'fac':
            print(f"*Warning*: {checkout} is over the {user} limit.")
            
        #grad limit is 50
        elif checkout >= 50 and user == 'grad':
            print(f"{checkout} is over the {user} limit.")
        
        else:
            print(f"{checkout} is under the {user} limit.")
    
    # print an empty line between users
    print()
    
```
```output
3 is under the fac limit.
50 is under the fac limit.
*Warning*: 120 is over the fac limit.

3 is under the grad limit.
*Warning*: 50 is over the grad limit.
*Warning*: 120 is over the grad limit.
```

:::::::::::::::::::::::::::::::::::::::  challenge

## Age conditionals

Write a Python program that checks the age of a user to determine if they will receive a youth or adult library card. The program should:

1. Store `age` in a variable.
2. Use an `if` statement to check if the age is 16 or older. If true, print "You are eligible for an adult library card."
3. Use an `else` statement to print "You are eligible for a youth library card" if the age is less than 16.

If you finish early, try this challenge: 

- In a new cell, adapt your program to loop through a list of age values, testing each age with the same output as above.

:::::::::::::::  solution

## Solution

For parts 1 to 3:

```python
age = 25

if age >= 16:
  print('You are eligible for an adult library card.')
else:
  print('You are eligible for a youth library card.')
```

For the challenge:
```python
ages = [10, 16, 30, 65]

for age in ages:
  if age >= 16:
    print('You are eligible for an adult library card.')
  else:
    print('You are eligible for a youth library card.')
```


:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::  challenge

## Conditional logic: Fill in the blanks

Fill in the blanks in the following program to check if both the name variable is present in the names list and the password variable is equal to 'true' before giving a user access to a library system.

If you have extra time after you solve the fill in the blanks, change the value of `password` and re-run the program to view the output. 

```python
names = ['Wang', 'Garcia', 'Martin']
name = 'Martin'
password = 'true'

___ item in names:
    print(item)
    if name == item ___ password == _____:
        print('Login successful!')
    elif password __ 'true':
        print(f'Your password is incorrect. Try again.')
    ____ name __ item:
        print(f'- Name does not match. Testing the next item in the list for {name}...')
  
```
:::::::::::::::  solution

## Solution

```python
names = ['Wang', 'Garcia', 'Martin']
name = 'Martin'
password = 'true'

for item in names:
    print(item)
    if name == item and password == 'true':
        print('Login successful!')
    elif password != 'true':
        print(f'Your password is incorrect. Try again.')
    elif name != item:
        print(f'- Name does not match. Testing the next item in the list for {name}...')
```

```output
Wang
- Name does not match. Testing the next item in the list for Martin...
Garcia
- Name does not match. Testing the next item in the list for Martin...
Martin
Login successful!
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Processing Files Based on Record Length

Modify this program so that it only processes files with fewer than 85 records.

```python
import glob
import pandas
for filename in glob.glob('data/*.csv'):
    contents = pandas.read_csv(filename)
    ____ ___(______) < ____:
        print(f'{filename} : {len(contents)}')
```

:::::::::::::::  solution

## Solution

```python
import glob
import pandas
for filename in glob.glob('data/*.csv'):
   contents = pandas.read_csv(filename)
   if len(contents) < 85:
       print(f'{filename} : {len(contents)}')
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use `if` statements to control whether or not a block of code is executed.
- Conditionals are often used inside loops.
- Use `else` to execute a block of code when an `if` condition is *not* true.
- Use `elif` to specify additional tests.
- Conditions are tested once, in order.
- Use `and` and `or` to check against multiple value statements.

::::::::::::::::::::::::::::::::::::::::::::::::::


