---
title: Data Types and Type Conversion
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Explain key differences between integers and floating point numbers.
- Explain key differences between numbers and character strings.
- Use built-in functions to convert between integers, floating point numbers, and strings.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- What kinds of data do programs store?
- How can I convert one type to another?

::::::::::::::::::::::::::::::::::::::::::::::::::

## Every value has a type.

- Every value in a program has a specific type.
- Integer (`int`): whole numbers like 3 or -512.
- Floating point number (`float`): fractional numbers like 3.14159 or -2.5.
- Whole numbers may also be stored as floats, e.g. `1.0`, but `1.0` would still be stored as a `float`.
- Character string (usually called "string", `str`): text.
  - Written in either single quotes or double quotes (as long as they match).
  - The quotation marks aren't printed using `print()`, but may appear when viewing a value in the Jupyter Notebook or other Python interpreter.

## Use the built-in function `type` to find the type of a value.

- Use the built-in function `type` to find out what type a value has.
- This works on variables as well.
  - But remember: the *value* has the type --- the *variable* is just a label.
  - When you change the value of a variable to a new data type, the results of `print(type(your_variable))` will change accordingly.

```python
print(type(52))
```

```output
<class 'int'>
```

```python
title = 'Biochemistry'
print(type(title))
```

```output
<class 'str'>
```

## Types control what operations (or methods) can be performed on a given value.

- A value's type determines what the program can do to it.

```python
print(5 - 3)
```

```output
2
```

```python
print('hello' - 'h')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-2-67f5626a1e07> in <module>()
----> 1 print('hello' - 'h')

TypeError: unsupported operand type(s) for -: 'str' and 'str'
```

## You can use the `+` and `*` operators on strings.

- "Adding" character strings concatenates them.

```python
full_name = 'Ahmed' + ' ' + 'Walsh'
print(full_name)
```

```output
Ahmed Walsh
```

- Multiplying a character string by an integer *N* creates a new string that consists of that character string repeated  *N* times.
  - Since multiplication is repeated addition.
- There are more ways that traditional math operators will work on other data types.  There isn't a perfect formula for figuring out what they do, so experimentation is valuable.

```python
separator = '=' * 10
print(separator)
```

```output
==========
```

## Strings have a length (but numbers don't).

- The built-in function `len` counts the number of characters in a string.

```python
print(len(full_name))
```

```output
11
```

- But numbers don't have a length (not even zero).

```python
print(len(52))
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-3-f769e8e8097d> in <module>()
----> 1 print(len(52))

TypeError: object of type 'int' has no len()
```

## Must convert numbers to strings or vice versa when operating on them.

- Cannot add numbers and strings.

```python
print(1 + 'A')
```

```error
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-fe4f54a023c6> in <module>()
----> 1 print(1 + '2')

TypeError: unsupported operand type(s) for +: 'int' and 'str'
```

- Not allowed because it's ambiguous: should `1 + '2'` be `3` or `'12'`?
- Some types can be converted to other types by using the type name as a function.

```python
print(1 + int('2'))
print(str(1) + '2')
```

```output
3
12
```

## Can mix integers and floats freely in operations.

- Integers and floating-point numbers can be mixed in arithmetic.
  - Python automatically converts integers to floats as needed.

```python
print('half is', 1 / 2.0)
print('three squared is', 3.0 ** 2)
```

```output
half is 0.5
three squared is 9.0
```

## Variables only change value when something is assigned to them.

- If we make one cell in a spreadsheet depend on another,
  and update the latter,
  the former updates automatically.
- This does **not** happen in programming languages.

```python
first = 1
second = 5 * first
first = 2
print('first is', first, 'and second is', second)
```

```output
first is 2 and second is 5
```

- The computer reads the value of `first` when doing the multiplication,
  creates a new value, and assigns it to `second`.
- After that, `second` does not remember where it came from.

:::::::::::::::::::::::::::::::::::::::  challenge

## Fractions

What type of value is 3.4?
How can you find out?

:::::::::::::::  solution

## Solution

It is a floating-point number (often abbreviated "float").

```python
print(type(3.4))
```

```output
<class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Automatic Type Conversion

What type of value is 3.25 + 4?

:::::::::::::::  solution

## Solution

It is a float:
integers are automatically converted to floats as necessary.

```python
result = 3.25 + 4
print(result, 'is', type(result))
```

```output
7.25 is <class 'float'>
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Choose a Type

What type of value (integer, floating point number, or character string)
would you use to represent each of the following?  Try to come up with more than one good answer for each problem.  For example, in  # 1, when would counting days with a floating point variable make more sense than using an integer?

1. Number of days since the start of the year.
2. Time elapsed since the start of the year.
3. Call number of a book.
4. Standard book loan period.
5. Number of reference queries in a year.
6. Average library classes taught per semester.

:::::::::::::::  solution

## Solution

1. Integer
2. Float
3. String
4. Integer
5. Integer
6. Float  
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Division Types

There are three different types of division:

1. 'Normal' division (aka floating-point division) is what most people may be
  familiar with: 5 / 2 = 2.5
2. Floor division, which cuts out the part after the period: 5 / 2 = 2
3. Modulo division, which only keeps the remained after division: 5 / 2 = 1

In Python 3,  the `/` operator performs floating-point division, the `//`
operator performs floor division, and the '%' (or *modulo*) operator
calculates the modulo division:

```python
print('5 / 3:', 5/3)
print('5 // 3:', 5//3)
print('5 % 3:', 5%3)
```

```output
5 // 3: 1
5 / 3: 1.6666666666666667
5 % 3: 2
```

If `num_students` is the number of students enrolled in a course (let say 600),
and `num_per_class` is the number that can attend a single class (let say 42),
write an expression that calculates the number of classes needed
to teach everyone.

:::::::::::::::  solution

## Solution

Depending on requirements it might be important to detect when the number of students per class doesn't divide the
number of students evenly. Detect it with the `%` operator and test if the remainder that it returns is greater than
0\.

```python
num_students = 600
num_per_class = 42
num_classes = num_students // num_per_class
remainder = num_students % num_per_class

print(num_students, 'students,', num_per_class, 'per class')
print(num_classes, ' full classes, plus an extra class with only ', remainder, 'students')
```

```output
600 students, 42 per class
14  full classes, plus an extra class with only  12 students
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Strings to Numbers

Where reasonable, `float()` will convert a string to a floating point number,
and `int()` will convert a floating point number to an integer:

```python
print("string to float:", float("3.4"))
print("float to int:", int(3.4))
```

```output
string to float: 3.4
float to int: 3
```

**Note:** conversion is some times also called typecast.

If the conversion doesn't make sense, however, an error message will occur

```python
print("string to float:", float("Hello world!"))
```

```error
---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-5-df3b790bf0a2> in <module>()
----> 1 print("string to float:", float("Hello world!"))

ValueError: could not convert string to float: 'Hello world!'
```

Given this information, what do you expect the following program to do?

What does it actually do?

Why do you think it does that?

```python
print("fractional string to int:", int("3.4"))
```

:::::::::::::::  solution

## Solution

What do you expect this program to do? It would not be so unreasonable to
expect the Python `int` command to convert the string "3.4" to 3.4 and an
additional type conversion to 3. After all, Python performs a lot of other
magic - isn't that part of its charm?

However, Python throws an error. Why? To be consistent, possibly. If you
ask Python to perform two consecutive typecasts, you must convert it
explicitly in code.

```python
num_as_string = "3.4"
num_as_float = float(num_as_string)
num_as_int = int(num_as_float)
print(num_as_int)
```

```output
3
```

We could also write it in a single line like this: `int(float("3.4"))`



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Arithmetic with Different Types

Which of the following will print 2.0?
Note: there may be more than one right answer.

```python
first = 1.0
second = "1"
third = "1.1"
```

1. `first + float(second)`
2. `float(second) + float(third)`
3. `first + int(third)`
4. `first + int(float(third))`
5. `int(first) + int(float(third))`
6. `2.0 * second`

:::::::::::::::  solution

## Solution

Answer: 1 and 4.

1. is correct
2. gives 2.1
3. gives an error because we cannot convert text to int directly
4. is correct
5. gives 2 (as an integer not as a float)
6. gives an error because `second` is a string.
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- Every value has a type.
- Use the built-in function `type` to find the type of a value.
- Types control what operations can be done on values.
- Strings can be added and multiplied.
- Strings have a length (but numbers don't).
- Must convert numbers to strings or vice versa when operating on them.
- Can mix integers and floats freely in operations.
- Variables only change value when something is assigned to them.

::::::::::::::::::::::::::::::::::::::::::::::::::


