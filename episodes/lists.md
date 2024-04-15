---
title: Lists
teaching: 10
exercises: 10
---

::::::::::::::::::::::::::::::::::::::: objectives

- Create collections to work with in Python using lists.
- Write Python code to index, slice, and modify lists through assignment and method calls.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- How can I store multiple items in a Python variable?

::::::::::::::::::::::::::::::::::::::::::::::::::

## A list stores many values in a single structure.
The most popular kind of data collection in Python is the list. Lists have two primary important characteristics:

1. They are mutable, i.e., they can be changed after they are created.
2. They are heterogeneous, i.e., they can store values of many different types.

In the dataset we will be working with soon, we'll look at the circulation numbers from a variety of branch libraries in Chicago, Illinois (USA). Each branch library has some metadata associated with it, including its zip (postal) code. We could use a Python list to organize some of those zip codes.

To create a new list, you can just put some values in square brackets with commas in between.

```python
zip_codes = [60625, 60827, 60632, 60644, 60634]
f'Zip codes: {zip_codes}'
```

```output
'Zip codes: [60625, 60827, 60632, 60644, 60634]'
```

We can use `len()` to find out how many values are in a list.

```python
f'Number of zip codes: {len(zip_codes)}'
```

```output
'Number of zip codes: 5'
```

## Use an item's index to fetch it from a list.

In the same way we used index numbers for strings, we can reference elements and slices in a list.

```python
print(f'1st item of zip_codes: {zip_codes[0]}')
print(f'The first three zip codes: {zip_codes[0:3]}')
```

```output
1st item of zip_codes: 60625
The first three zip codes: [60625, 60827, 60632]
```

## Reassign list values with their index.

Use an index value along with your list variable to replace a value from the list.

```python
print(f'zip_codes was: {zip_codes}')
zip_codes[0] = 60640
print(f'zip_codes is now: {zip_codes}')
```

```output
zip_codes was: [60625, 60827, 60632, 60644, 60634]
zip_codes is now: [60640, 60827, 60632, 60644, 60634]
```


### Character strings are immutable.

Unlike lists, we cannot change the characters in a string using its index value. In other words strings are *immutable* (cannot be changed in-place after creation), while lists are *mutable*: they can be modified in place. Python considers the string to be a single value with parts, not a collection of values.

```python
branch_library = 'Ulbany Park' # misspelled Albany
branch_library[0] = 'A'
```

```error
TypeError: 'str' object does not support item assignment
```

## Lists may contain values of different types.

A single list may contain numbers, strings, and anything else (including other lists!). If you're dealing with a list within a list you can continue to use the square bracket notation to reference specific items.

```python
mixed_list = ['word', 3, 10.2, ['list', 'of', 'items']]
print(f'1st word in sublist: {mixed_list[3][0]}')
```

```output
1st word in sublist: list
```

## Appending items to a list lengthens it.

Use `list_name.append` to add items to the end of a list. In Python, we would call `.append()` a *method* of the list object. You can use the syntax of `object.method()` to call methods.

```python
print(f'zip_codes was:{zip_codes}')
zip_codes.append(60647)
print(f'zip_codes is now: {zip_codes}')
```

```output
zip_codes was: [60640, 60827, 60632, 60644, 60634]
zip_codes is now: [60640, 60827, 60632, 60644, 60634, 60647]
```

## Use `del` to remove items from a list entirely.

`del list_name[index]` removes an item from a list and shortens the list. Unlike `.append()`, `del` is not a method, but a statement in Python. In the example below, `del` performs an "in-place" operation on a list of prime numbers. This means that the `primes` variable will be reassigned when you use the `del` statement, without needing to use an assignment operator (e.g., `primes = ...`) .

```python
primes = [2, 3, 5, 7, 11]
print(f'primes before removing last item: {primes}')
del primes[4]
print(f'primes after removing last item: {primes}')
```

```output
primes before removing last item: [2, 3, 5, 7, 11]
primes after removing last item: [2, 3, 5, 7]
```


:::::::::::::::::::::::::::::::::::::::  challenge

## Fill in the Blanks

Fill in the blanks so that the program below produces the output shown. (Hint: Use [] on its own to represent a list that doesn’t contain any values.)

```python
values = ____
values.____(1)
values.____(3)
values.____(5)
print('first time:', values)
values = values[____]
print('second time:', values)
```

```output
first time: [1, 3, 5]
second time: [3, 5]
```

:::::::::::::::  solution

## Solution

```python
values = []
values.append(1)
values.append(3)
values.append(5)
print('first time:', values)
values = values[1:3]
print('second time:', values)
```

```output
first time [1, 3, 5]
second time [3, 5]
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## How Large is a Slice?

If 'low' and 'high' are both non-negative integers,
how long is the list returned by this slicing operation `values[low:high]`?

:::::::::::::::  solution

## Solution

The list's length would be equal to `high - low`.  



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## From Strings to Lists and Back

Given this:

```python
print('string to list:', list('book'))
print('list to string:', ''.join(['a', 'r', 't', 'i', 'c', 'l', 'e']))
```

```output
['b', 'o', 'o', 'k']
'article'
```

1. Explain in simple terms what `list('some string')` does.
2. What does `'-'.join(['x', 'y'])` generate? Note that the first set of single quotes is not empty.

:::::::::::::::  solution

## Solution

1. It creates a list of the `some string`s characters as elements.
2. It creates a string composed of `x` and `y`, separated by a hyphen character(`-`).  
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Working With the End

What does the following program print?

```python
resources = ['books','periodicals','DVDs','maps',
'databases','abstracts']
print(resource[-1])
```

1. How does Python interpret a negative index?
2. If a list or string has N elements,
  what is the most negative index that can safely be used with it,
  and what location does that index represent?
3. If `resources` is a list, what does `del resources[-1]` do?
4. How can you display all elements but the last one without changing `resources`?
  (Hint: you will need to combine slicing and negative indexing.)

:::::::::::::::  solution

## Solution

```output
abstracts
```

1. A negative index begins at the final element.
2. `-(N)` corresponds to the first index, which is the [0] index.
3. It removes the final element of the list.
4. You could do the following: `print(resources[0:-1])`
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Stepping Through a List

What does the following program print?

```python
resources = ['books','periodicals','DVDs','maps',
'databases','abstracts'] 
print(resources[::2])
print(resources[::-1])
```

1. If we write a slice as `low:high:stride`, what does `stride` do?
2. What expression would select all of the even-numbered items from a collection?

:::::::::::::::  solution

## Solution

```output
['books', 'DVDs', 'databases']
['abstracts', 'databases', 'maps', 'DVDs', 'periodicals', 'books']
```

1. `stride` indicates both the number of steps, and from which end: positive starts from first element, negative from the last element.
2. `resources[1::2]`
  
  

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Slice Bounds

What does the following program print?

```python
resources = ['books','periodicals','DVDs','maps',
'databases','abstracts'] 
print(resources[0:20])
print(resources[-1:3])
```

:::::::::::::::  solution

## Solution

```output
['books', 'periodicals', 'DVDs', 'maps', 'databases', 'abstracts']
[]
```

There is no 20th index, so the entire list is captured.  
There is no element after the -1 index, so an empty list is returned as empty square brackets.  



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::  challenge

## Sort and Sorted

What do these two programs print?
In simple terms, explain the difference between `sorted(resources)` and `resources.sort()`.

```python
# Program A
resources =  ['books','periodicals','DVDs','maps',
'databases','abstracts'] 
result = sorted(resources)
print('resources is', resources, 'and result is', result)
```

```python
# Program B
resources = ['books','periodicals','DVDs','maps',
'databases','abstracts'] 
result = resources.sort()
print('resources is', resources, 'and result is', result)
```

:::::::::::::::  solution

## Solution

Program A:

```output
resources is ['books', 'periodicals', 'DVDs', 'maps', 'databases', 'abstracts'] and result is ['DVDs', 'abstracts', 'books', 'databases', 'maps', 'periodicals']
```
Notice that the capital letters in acronym DVD sort before lowercase letters.

Program B:

```output
resources is ['DVDs', 'abstracts', 'books', 'databases', 'maps', 'periodicals'] and result is None
```

`sorted(resources)` returns a sorted copy of the list, while `resources.sort()` function call sorts the list *in place* and returns `None`.  



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::::: keypoints

- A list stores many values in a single structure.
- Use an item's index to fetch it from a list.
- Lists' values can be replaced by assigning to them.
- Appending items to a list lengthens it.
- Use `del` to remove items from a list entirely.
- The empty list contains no values.
- Lists may contain values of different types.
- Character strings can be indexed like lists.
- Character strings are immutable.
- Indexing beyond the end of the collection is an error.

::::::::::::::::::::::::::::::::::::::::::::::::::


