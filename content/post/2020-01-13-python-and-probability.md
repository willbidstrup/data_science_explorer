---
title: Python and probability
author: Will Bidstrup
date: '2020-01-13'
slug: python-and-probability
categories:
  - Python
tags:
  - Python
---
This is a notebook for practicing Python and testing some probability problems.

# Things to remember Python vs R

Python indents and spacing matter  
Python no curly braces in functions  
Python is 0 indexed    
Python can multiply strings 
Python is left inclusive and right exclusive  
Python is object oriented 
Python "." are important  
Python pass objects to functions and use methods on objects    
Lists and dictionaries are important  
Create list with []   
Create dictionary to store key:value pairs with {}   
Use numpy for arrays and matrices  
Use pandas for dataframes  



# Functions

I will start by creating some functions for counting combinations and permutations.  


```python
# Use a package for factorial

import math

print(math.factorial(4)) # Must explicitly call print in Python
```


```python
# Create a function for combinations

def combination(n, k = 2): # No curly braces, indentation and whitespace matter
            """ Insert text here"""
            combinations = math.factorial(n) / ((math.factorial(n - k)) * math.factorial(k))
            return combinations # No automatic return, must be explicit
    
```


```python
# Test the combination function

print(combination(2)) # From 2 choose 2, order doesn't matter

print(combination(3)) # From 3 choose 2, order doesn't matter

print(combination(4)) # From 4 choose 2, order doesn't matter

print(combination(5)) # From 5 choose 2, order doesn't matter

print(combination(5,3)) # From 5 choose 3, order doesn't matter
```

    1.0
    3.0
    6.0
    10.0
    10.0



```python
# Create a function for permutations

def permutation(n, k = 2): # No curly braces, indentation and whitespace matter
            """ Insert text here"""
            permutations = math.factorial(n) / math.factorial(n - k)
            return permutations # No automatic return, must be explicit
    
```


```python
# Test the permutation function

print(permutation(2)) # From 2 choose 2, order does matter

print(permutation(3)) # From 3 choose 2, order does matter

print(permutation(4)) # From 4 choose 2, order does matter

print(permutation(5)) # From 5 choose 2, order does matter

print(permutation(5, 3)) # From 5 choose 3, order does matter
```

    2.0
    6.0
    12.0
    20.0
    60.0


# Applying function to a list 

I want to create a list of combinations and a list of permutations.  


```python
# Create list of numbers and amount to be chosen

number_list = list(range(2, 11)) # Numbers from 2 to 10
choose_list = [2] * 9 # Number 2 repeated 9 times
```


```python
print(number_list)
print(choose_list)
```

    [2, 3, 4, 5, 6, 7, 8, 9, 10]
    [2, 2, 2, 2, 2, 2, 2, 2, 2]



```python
# Run combination function across all numbers in number_list - FOR LOOP METHOD

combinations_list_forloop = [] # Create an empty list

for x in number_list:
    combinations_list_forloop.append(combination(x))
print(combinations_list)
                                          
```

    [1.0, 3.0, 6.0, 10.0, 15.0, 21.0, 28.0, 36.0, 45.0]



```python
# Run combination function across all numbers in number_list - COMPREHENSION METHOD

combinations_list_comprehension = [combination(x) for x in number_list]

print(combinations_list_comprehension )
                         
```

    [1.0, 3.0, 6.0, 10.0, 15.0, 21.0, 28.0, 36.0, 45.0]



```python
# Run combination function across all numbers in number_list - MAP METHOD

combinations_list_map = list(map(combination, number_list))
print(combinations_list_map)
```

    [1.0, 3.0, 6.0, 10.0, 15.0, 21.0, 28.0, 36.0, 45.0]


# Create a data frame


```python
# Create the desired columns

column_1 = number_list
print(column_1)

column_2 = list(map(combination, number_list))
print(column_2)

column_3 = list(map(permutation, number_list))
print(column_3)
```

    [2, 3, 4, 5, 6, 7, 8, 9, 10]
    [1.0, 3.0, 6.0, 10.0, 15.0, 21.0, 28.0, 36.0, 45.0]
    [2.0, 6.0, 12.0, 20.0, 30.0, 42.0, 56.0, 72.0, 90.0]



```python
# Import pandas

import pandas as pd
```


```python
# Create data frame containing combinations and permutations - DICTIONARY METHOD

probability_df = pd.DataFrame({
            "Number": column_1,
            "Combinations": column_2,
            "Permutations": column_3})
```


```python
print(probability_df)
```

       Number  Combinations  Permutations
    0       2           1.0           2.0
    1       3           3.0           6.0
    2       4           6.0          12.0
    3       5          10.0          20.0
    4       6          15.0          30.0
    5       7          21.0          42.0
    6       8          28.0          56.0
    7       9          36.0          72.0
    8      10          45.0          90.0

