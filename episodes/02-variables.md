---
title: Variables and Strings
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Write programs that assign values to variables and perform calculations with those values.
- Use indexing to manipulate elements within a string.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I store data in Python?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Use variables to store values.

Variables are names given to certain values. In Python the `=` symbol assigns a value on the right to the name on the left. A variable is created when a value is assigned to it. Here, Python assigns the number `42` to the variable `age` and the name `Ahmed` in quotation marks to a variable `first_name`.

```python
age = 42
first_name = 'Ahmed'
```

- Variable names:
  - cannot start with a digit
  - cannot contain spaces, quotation marks, or other punctuation
  - *may* contain an underscore (typically used to separate words in long variable names)
  - are case sensitive. `first_name` and `First_Name` would be different variables.

## Use `print()` to display values.

Python has a built-in function called `print()` to display Python objects to the display. You can print Python objects to the Jupyter notebook output using the built-in function, `print()`. Inside of the parentheses we can add the Python objects that we want print, which are known as the `print()` function's arguments. You can pass variables and text strings (by placing text within quotation marks) directly to the print function, and you can separate multiple items with commas. 

```python
print(first_name, 'is', age, 'years old')
```

```output
Ahmed is 42 years old
```

`print()` automatically puts a single space between items to separate them, and add a new line at the end of every printout.

## Variables must be created before they are used.

If a variable doesn't exist yet, or if the name has been misspelled, Python reports an error.

```python
print(eye_color)
```

```error
---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-1-c1fbb4e96102> in <module>()
----> 1 print(eye_color)

NameError: name 'eye_color' is not defined
```

The last line of an error message is usually the most informative. In this case it tells us that the `eye_color` variable is not defined. NameErrors often refer to variables that haven't been assigned yet.

:::::::::::::::::::::::::::::::::::::::::  callout

## Variables Persist Between Cells

Variables defined in one cell exist in all other cells once they have been executed, so the relative location of cells in the notebook do not matter. In other words if you execute a cell at the bottom of your notebook, the variables in the cell will be available afterwards in cells at the top of the notebook.
Notebook cells are a way to organize your code, but Python only cares about the order in which the code has been executed.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Variables can be used in calculations.

We can use variables in calculations just as if they were values. We assigned 42 to `age` a few lines ago, so we can reference that value within a new variable assignment.

```python
age = age + 3
print('Age in three years:', age)
```

```output
Age in three years: 45
```

## Use an index to get a single character from a string.

We can reference the specific location of a character (individual letters, numbers, and so on) in a text string by using its index position. In Python, each character in a string (first, second, etc.) is given a number, which is called an index. Indices are numbered to begin from 0 rather than 1. We can use an index number in square brackets to refer to the character at that position.

```python
element = 'helium'
print(element[0])
```

```output
h
```

## Use a slice to get multiple characters from a string.

A slice is a part of a string that we can reference using `[start:stop]`, where `start` is the index of the first character we want and `stop` is the last character. Referencing a string slice does not change the contents of the original string. Instead, the slice returns a copy of the part of the original string we want. 

```python
element = 'sodium'
print(element[0:3])
```

```output
sod
```

Note that in the example above, `element[0:3]` begins with zero, which refers to the first element in the string, and ends with a 3. When working with slices the end point is interpreted as going up to, *but not including* the index number provided. In other words, the character in the index position of 3 in the string `sodium` is `i`, so the slice `[0:3]` will go up to but not include that character, and therefore give us `sod`.

## Use the built-in function `len` to find the length of a string.

The `len()`function will tell us the length of an item. In the case of a string, it will tell us how many characters are in the string. 

```python
print(len('helium'))
```

```output
6
```

In the example above we have nested the `print()` and `len()` functions. When nesting functions, they are evaluated from the inside out, just like in mathematics, so `len()` is evaluated first, followed by the `print()` function.


## Use meaningful variable names. 
Python doesn't care what you call variables as long as they obey the rules (alphanumeric characters and the underscore).

```python
flabadab = 42
ewr_422_yY = 'Ahmed'
print(ewr_422_yY, 'is', flabadab, 'years old')
```

But it's important to use meaningful variable names to help other people understand what the program does. Often, the most important "other person" is your future self.

:::::::::::::::::::::::::::::::::::::::  challenge

## Swapping Values

Draw a table showing the values of the variables in this program
after each statement is executed.
In simple terms, what do the last three lines of this program do?

```python
x = 1.0
y = 3.0
swap = x
x = y
y = swap
```

:::::::::::::::  solution

## Solution

```
swap = x  #  x->1.0 y->3.0 swap->1.0
x = y     #  x->3.0 y->3.0 swap->1.0
y = swap  #  x->3.0 y->1.0 swap->1.0
```

These three lines exchange the values in `x` and `y` using the `swap`
variable for temporary storage. This is a fairly common programming idiom.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Predicting Values

What is the final value of `position` in the program below?
(Try to predict the value without running the program,
then check your prediction.)

```python
initial = "left"
position = initial
initial = "right"
```

:::::::::::::::  solution

## Solution

```python
initial = "left"  # Initial is assigned the string "left"
position = initial  # Position is assigned the variable initial, currently "left"
initial = "right"  # Initial is assigned the string "right"
print(position)
```

```output
left
```

The last assignment to position was "left"



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Can you slice integers?

If you assign `a = 123`,
what happens if you try to get the second digit of `a`?

:::::::::::::::  solution

## Solution

Numbers are not stored in the written representation,
so they can't be treated like strings.

```python
a = 123
print(a[1])
```

```error
TypeError: 'int' object is not subscriptable
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Choosing a Name

Which is a better variable name, `m`, `min`, or `minutes`?
Why?
Hint: think about which code you would rather inherit
from someone who is leaving the library:

1. `ts = m * 60 + s`
2. `tot_sec = min * 60 + sec`
3. `total_seconds = minutes * 60 + seconds`

:::::::::::::::  solution

## Solution

`minutes` is better because `min` might mean something like "minimum"
(and actually does in Python, but we haven't seen that yet).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Slicing

We know how to slice using an explicit start and end point:

```python
library_name = 'Library of Babel'
print('library_name[1:3] is:', library_name[1:3])
```
```output
library_name[1:3] is: ib
```

But we can also use implicit and negative index values when we define a slice. Try the following (replacing `low` and `high` with index positions of your choosing) to figure out how these different forms of slicing work:

1. What does `library_name[low:]` (without a value after the colon) do?
2. What does `library_name[:high]` (without a value before the colon) do?
3. What does `library_name[:]` (just a colon) do?
4. What does `library_name[number:negative-number]` do?

:::::::::::::::  solution

## Solution

1. It will slice the string, starting at the `low` index and stopping at the end of the string
2. It will slice the string, starting at the beginning on the string, and ending an element before the `high` index
3. It will print the entire string
4. It will slice the string, starting the `number` index, and ending a distance of the absolute value of `negative-number` elements from the end of the string
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Use variables to store values.
- Use `print` to display values.
- Variables persist between cells.
- Variables must be created before they are used.
- Variables can be used in calculations.
- Use an index to get a single character from a string.
- Use a slice to get a portion of a string.
- Use the built-in function `len` to find the length of a string.
- Python is case-sensitive.
- Use meaningful variable names.

::::::::::::::::::::::::::::::::::::::::::::::::::


