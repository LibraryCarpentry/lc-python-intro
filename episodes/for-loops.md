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

One way to print each number is to use a `print` statement with the index value for each item in the list:

```python
print(odds[0], odds[1], odds[2], odds[3])
```

```output
1 3 5 7
```

This is a bad approach for three reasons:

1. **Not scalable**. Imagine you need to print a list that has hundreds
  of elements.  

2. **Difficult to maintain**. If we want to add another change -- multiplying each number by 5, for example -- we would have to change the code for every item in the list, which isn't sustainable

3. **Fragile**. Hand-numbering index values for each item in a list is likely to cause errors if we make any mistakes.


```python
odds = [1, 3, 5]
print(odds[0], odds[1], odds[2], odds[3])
```

We get an IndexError when we try to refer to an item in a list that does not exist.

```error
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
<ipython-input-3-7974b6cdaf14> in <module>()
      3 print(odds[1])
      4 print(odds[2])
----> 5 print(odds[3])

IndexError: list index out of range
```

A `for` loop is a better solution:

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

A `for` loop repeats an operation -- in this case, printing -- once for each element it encounters in a collection. The general structure of a loop is:

```python
for variable in collection:
    # do things using variable, such as print
```

We can call the loop variable anything we like, there must be a colon at the end of the line starting the loop, and we must indent anything we want to run inside the loop. Unlike many other programming languages, there is no command to signify the end of the loop body; everything indented after the `for` statement belongs to the loop.

## Loop variables 

Loop variables are created on demand when you define the loop and they will persist after the loop finishes. In other words, in the loop:

```python
odds = [1, 3, 5, 7]
for num in odds:
    print(num)
print(num)
```
We are creating a new variable called `num` that will correspond to each element in the `odds` list as it passes through the loop. At the end of the loop, `num` is still equal to the last element in the list it was assigned to.

Like all variable names, it's helpful to give `for` loop variables meaningful names that you'll understand as the code in your loop grows. For example, `even` is probably a better variable to use than `kitten` here:


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

A common loop pattern is to initialize an *accumulator* variable to zero, an empty string, or an empty list before the loop begins. Then the loop updates the accumulator variable with values from a collection.

```python
# Sum the first 10 integers.
total = 0
for number in range(1, 11):
    print(f'number is: {number} total is: {total}')
    total = total + number
print(f'At the end of the loop, number is {number} and total is {total}')
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
At the end of the loop number is 10 and total is 55
```


:::::::::::::::::::::::::::::::::::::::  challenge

## Reversing a String

Fill in the blanks in the program below so that it prints "nit"
(the reverse of the original character string "tin"). 

Tip: you can concatenate two strings together using the `+` operator. For example, `'librar' + 'ian'` will create one string, `'librarian'`.

```python
original = "tin"
result = ____
for char in original:
    result = ____ _ _____
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
```
```output
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

Fill in the blanks to sum the lengths of each string in the list, `["book", "magazine", "dvd"]`

```python
# Total length of the strings in the list: ["book", "magazine", "dvd"] 
total = 0
for word in ["book", "magazine", "dvd"] :
    ____ = total + ___(word)
print(total)
```
:::::::::::::::  solution

## Solution

```python
total = 0
for word in ["book", "magazine", "dvd"] :
    total = total + len(word)
print(total)
```

```output
15
```

:::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Use slices in a loop

How would you loop through a list, `["red", "green", "blue"]` to create (and print out) the acronym `RGB`, pulling from the first letters in each string?

Tip: You can apply the .capitalize() function to capitalize the first letter of a string. For example, `'university'.capitalize()` will yield `'University'`.


:::::::::::::::  solution

## Solution

```python
acronym = ''
for color in ['red', 'green', 'blue']:
    acronym = acronym + color[0].capitalize()
print(acronym)
```

```output
RGB
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Use range() in a loop

How would you create a list including the numbers 1, 2, 3, 4, 5, 6, 7, 8, 9, and 10, using range() in a `for` loop?

Tips: 

- You can create a blank list before the `for` loop by assigning a variable to `[]`. For example, `container_list = []`.
- You can use the .append() method to add items to a list.

:::::::::::::::  solution

## Solution

```python
container = []
for num in range(1, 11):
    container.append(num)
print(container)
    
```

```output
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

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


