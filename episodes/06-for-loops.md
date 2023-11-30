---
title: For Loops
teaching: 10
exercises: 15
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain what "for loops"" are normally used for.
- Trace the execution of an un-nested loop and correctly state the values of variables in each iteration.
- Write for loops that use the accumulator pattern to aggregate values.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I execute Python code iteratively across a collection of values?

::::::::::::::::::::::::::::::::::::::::::::::::::

## For loops

Let's create a short list of numbers in Python, and then attempt to print out each value in the list. 

```python
odds = [1, 3, 5, 7]
```

One way to print each number is to use four `print` statements--if you recall from episode 4--using the index values of each item in the list:

```python
print(odds[0])
print(odds[1])
print(odds[2])
print(odds[3])
```

```output
1
3
5
7
```

This is a bad approach for three reasons:

1. **Not scalable**. Imagine you need to print a list that has hundreds
  of elements.  

2. **Difficult to maintain**. If we want to add another change -- multiplying each number by 5, for example -- we would have to change four lines of code, which isn't sustainable

3. **Fragile**. Hand-numbering index values for each item in a list is likely to cause errors if we make any mistakes.

```python
odds = [1, 3, 5]
print(odds[0])
print(odds[1])
print(odds[2])
print(odds[3])
```

```output
1
3
5
```

```error
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-3-7974b6cdaf14> in <module>()
      3 print(odds[1])
      4 print(odds[2])
----> 5 print(odds[3])

IndexError: list index out of range
```

A `for loop` is a better solution:

```python
odds = [1, 3, 5, 7]
for num in odds:
    print(num)
```

```output
1
3
5
7
```

This code is shorter, and more robust as well. Even if the values of the `odds` list changes, the loop will still work.

```python
odds = [1, 3, 5, 7, 9, 11]
for num in odds:
    print(num)
```

```output
1
3
5
7
9
11
```

A `for loop` repeats an operation -- in this case, printing -- once for each element it encounters in a collection. The general structure of a loop is:

```python
for variable in collection:
    # do things using variable, such as print
```

We can call the loop variable anything we like, there must be a colon at the end of the line starting the loop, and we must indent anything we want to run inside the loop. Unlike many other languages, there is no command to signify the end of the loop body; everything indented after the `for` statement belongs to the loop.

## Loop variables 

Loop variables are created on demand when you define the loop and they will persist after the loop finishes. In other words, in the loop:

```python
odds = [1, 3, 5, 7]
for num in odds:
    print(num)
print(num)
```
We are creating a new variable called `num` that will correspond to each element in the `odds` list as it passes through the loop. At the end of the loop, `num` is still equal to the last element in the list it was assigned to.

Like all variable names, it's helpful to give for loop variables meaningful names that you'll understand as the code in your loop grows. For example, `even` is probably a better variable to use than `kitten` here:


```python
for kitten in [2, 4, 6, 8]:
    print(kitten)
```

## Use `range` to iterate over a sequence of numbers.

The built-in function `range()` produces a sequence of numbers. You can pass a single parameter to identify how many items in the sequence to range over (e.g. `range(5)`) or if you pass two arguments, the first corresponds to the starting point and the second to the end point. The end point works in the same way as Python index values ("up to, but not including").

```python
for number in range(0,3):
    print(number)
```

```output
0
1
2
```


## Accumulators

A common pattern for loops is to initialize an *accumulator* variable to zero, an empty string, or an empty list before the loop begins. Then the loop updates the accumulator variable with values from a collection.

```python
# Sum the first 10 integers.
total = 0
for number in range(1, 11):
    print('number is:', number, 'total is:', total)
    total = total + number
print('At the end of the loop')
print('number is:', number, 'total is:', total)
```

```output
number is: 1 total is: 0
number is: 2 total is: 1
number is: 3 total is: 3
number is: 4 total is: 6
number is: 5 total is: 10
number is: 6 total is: 15
number is: 7 total is: 21
number is: 8 total is: 28
number is: 9 total is: 36
number is: 10 total is: 45
At the end of the loop
number is: 10 total is: 55
```



:::::::::::::::::::::::::::::::::::::::  challenge

## Classifying Errors

Is an indentation error a syntax error or a runtime error?

:::::::::::::::  solution

## Solution

It is a syntax error. The problem has to do with the placement of the code, not its logic.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Tracing Execution

Create a table showing the numbers of the lines that are executed when this program runs,
and the values of the variables after each line is executed.

```python
total = 0
for char in "tin":
    total = total + 1
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Reversing a String

Fill in the blanks in the program below so that it prints "nit"
(the reverse of the original character string "tin").

```python
original = "tin"
result = ____
for char in original:
    result = ____
print(result)
```

:::::::::::::::  solution

## Solution

`result` is an empty string because we use it to build or accumulate on our reverse string. `char` is the loop variable for `original`. Each time through the loop `char` takes on one value from `original`. Use `char` with `result` to control the order of the string. Our loop code should look like this:

```
original = "tin"
result = ""
for char in original:
   result = char + result
print(result)
nit
```

If you were to expand out the loop the iterations would look something like this:

```python
#First loop
char = "t"
result = ""
char + result = "t"
#Second loop
char = 'i"
result = "t"
char + result = "it"
#Third loop
char = "n"
result = "it"
char + result = "nit"
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Practice Accumulating

Fill in the blanks in each of the programs below
to produce the indicated result.

```python
# Total length of the strings in the list: ["red", "green", "blue"] => 12
total = 0
for word in ["red", "green", "blue"]:
    ____ = ____ + len(word)
print(total)
```

```python
# List of word lengths: ["red", "green", "blue"] => [3, 5, 4]
lengths = ____
for word in ["red", "green", "blue"]:
    lengths.____(____)
print(lengths)
```

```python
# Concatenate all words: ["red", "green", "blue"] => "redgreenblue"
words = ["red", "green", "blue"]
result = ____
for ____ in ____:
    ____
print(result)
```

```python
# Create acronym: ["red", "green", "blue"] => "RGB"
# write the whole thing
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Cumulative Sum

Reorder and properly indent the lines of code below
so that they print an array with the cumulative sum of data.
The result should be `[1, 3, 5, 10]`.

```python
cumulative += [sum]
for number in data:
cumulative = []
sum += number
print(cumulative)
sum = 0
data = [1,2,2,5]
```

:::::::::::::::  solution

## Solution

```python
data = [1,2,2,5]
cumulative = []
sum = 0
for number in data:
  sum += number
  cumulative += [sum]
print(cumulative)
```

```output
[1, 3, 5, 10]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Identifying Variable Name Errors

1. Read the code below and try to identify what the errors are
  *without* running it.
2. Run the code and read the error message.
  What type of `NameError` do you think this is?
  Is it a string with no quotes, a misspelled variable, or a
  variable that should have been defined but was not?
3. Fix the error.
4. Repeat steps 2 and 3, until you have fixed all the errors.

```python
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (Number % 3) == 0:
        message = message + a
    else:
        message = message + "b"
print(message)
```

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Identifying Item Errors

1. Read the code below and try to identify what the errors are
  *without* running it.
2. Run the code, and read the error message. What type of error is it?
3. Fix the error.

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favorite season is ', seasons[4])
```

:::::::::::::::  solution

## Solution

It is an index error:

```error
IndexError: list index out of range
```

The problem is that `4` points to an item that doesn't exist in the list. Remember the first item of a list in Python is `0`.  
Replace `seasons[4]` with `seasons[0]`, `seasons[1]`, `seasons[2]` or `seasons[3]` to have the different items of the list printed.  



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- A *for loop* executes commands once for each value in a collection.
- The first line of the `for` loop must end with a colon, and the body must be indented.
- Indentation is always meaningful in Python.
- A `for` loop is made up of a collection, a loop variable, and a body.
- Loop variables can be called anything (but it is strongly advised to have a meaningful name to the looping variable).
- The body of a loop can contain many statements.
- Use `range` to iterate over a sequence of numbers.
- The Accumulator pattern turns many values into one.

::::::::::::::::::::::::::::::::::::::::::::::::::


