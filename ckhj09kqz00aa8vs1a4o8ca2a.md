## Peep into Python basics

This blog is written in Jupyter notebook, so you can experiment and learn by editing the notebook.   
Click  [here](https://github.com/kirankamatmgm/Interesting-Python/blob/main/Peep_into_pythonBasics.ipynb)  for notebook.

Just change the input and check the output.

Learning by experiment and hands-on exercises is always better.

The purpose of this notebook is just to revise python basics.

Let's get started.

### input is a built-in function in python

Get your name as an input and print it out on the screen 


```
name = input("Welcome! Welcome! Welcome!, What's your name: ")
print('Hello', name)
```

    Welcome! Welcome! Welcome!, What's your name: Kiran
    Hello Kiran


### Boolean values can be represented as one of two constant objects "False" and "True". 



```
# Booleans behave like integers 0 and 1.
True
```




    True




```
urMoney = 100
friendsMoney = 200
print(urMoney == friendsMoney)
```

    False


### List

A list is a collection which is ordered and changeable. 

List allows duplicate members.


```
my_list = ['Hello', 'Everyone', 'and', 'Welcome', 'to', 'Python', 'basics']
my_list
```




    ['Hello', 'Everyone', 'and', 'Welcome', 'to', 'Python', 'basics']




```
# Obtain the datatype
type(my_list)
```




    list




```
# list with mixed datatypes 
# (for example you can have strings and integers in one list)
# You can have a list inside another list (nested list)

my_list = ["GOOG", [3, 6, 7],"GOOG", [3, 6, 7],"GOOG", [3, 6, 7]]
my_list
```




    ['GOOG', [3, 6, 7], 'GOOG', [3, 6, 7], 'GOOG', [3, 6, 7]]




```
# Access specific elements in the list with Indexing
# Note that the first element in the list has an index of 0 (little confusing but you'll get used to it!)
my_list[1]
```




    [3, 6, 7]




```
# List Slicing (getting more than one element from a list) 

# obtain elements starting from index 3 up to and not including element with index 6  
print(my_list[3:6])
```

    [[3, 6, 7], 'GOOG', [3, 6, 7]]



```
# Obtain the length of the list (how many elements in the list) 
len(my_list)
```




    6



### Dictionary

my_dict = {'key1':'value1', 'key2':'value2', 'key3':'value3'}

Dictionary consists of a collection of key-value pairs. Each key-value pair maps the key to its corresponding value.

Keys are unique within a dictionary while values may not be. 

List elements are accessed by their position in the list, via indexing while Dictionary elements are accessed via keys



```
# Define a dictionary using key-value pairs
my_dict = {'key1':'value1',
           'key2':'value2', 
           'key3':'value3'}
```


```
# Check the data type
type(my_dict)
```




    dict




```
# Access specific element in the dictionary using a specific key (ex: Key2)
my_dict['key2']
```




    'value2'



### String



A string in Python is a sequence of characters

String can be enclosed by either double or single quotes


```
my_string = "Hello Everyone and Welcome to Python basics"
my_string
```




    'Hello Everyone and Welcome to Python basics'



Split is used to divide up the string into words 

The output from split is a list


```


x = my_string.split()
x
```




    ['Hello', 'Everyone', 'and', 'Welcome', 'to', 'Python', 'basics']



## Tuple

A tuple is a sequence of immutable Python objects. 

Tuples are sequences, just like lists. 

The differences between tuples and lists are, the tuples cannot be changed unlike lists and tuples use parentheses, whereas lists use square brackets.


```
tuple_1 = ('GOOGLE', 'APPLE', 10, 15, 1992);
tuple_2 = (450, 55, 977, 2100);
type(tuple_1)

```




    tuple




```
# Accessing elements in a tuple
tuple_1[1]
```




    'APPLE'




```
# Changing a vlue of a tuple does not work! 
# 'tuple' object does not support item assignment
tuple_1[1] = 0
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-18-0d93d25c1b58> in <module>()
          1 # Changing a vlue of a tuple does not work!
          2 # 'tuple' object does not support item assignment
    ----> 3 tuple_1[1] = 0
    

    TypeError: 'tuple' object does not support item assignment


## Set

A set is an unordered collection of items. Every element is unique (no duplicates).

A set is created by placing all the items (elements) inside curly braces {}, separated by comma or by using the built-in function set().



```

my_set = {'GOOGLE', 'APPLE', 'Jio'}
print(my_set)
```

    {'Jio', 'GOOGLE', 'APPLE'}



```
# set do not have duplicates
my_set = {'GOOG', 'APPL', 'T','TSLA','T','AAPL'}
print(my_set)
```

    {'GOOG', 'T', 'TSLA', 'AAPL', 'APPL'}


## If Else statements

- A simple if-else statement is written in Python as follows:

```
if condition:
  statement #1
else:
  statement #2
```

- If the condition is true, execute the first indented statement
- if the condition is not true, then execute the else indented statements. 
- Note that Python uses indentation (whitespace) to indicate code sections and scope.


```
if 10 > 9:
    print('If condition is True')
else:
    print('If condition is False')
```

    If condition is True


## Loops

For loops are used for iterating over a sequence (a list, a tuple, a dictionary, a set, or a string).

An action can be executed once for each item in a list, tuple of the for loop.

### For loop


```
for i in my_list:
    print(i)
```

    GOOG
    [3, 6, 7]
    GOOG
    [3, 6, 7]
    GOOG
    [3, 6, 7]


### Range() generates a list of numbers, which is used to iterate over with for loops.

range() is 0-index based, meaning list indexes start at 0, not 1. 

The last integer generated by range() is up to, but not including, last element. 

Example: range(0, 10) generates integers from 0 up to, but not including, 10.


```
for i in range(6):
    print(i)
```

    0
    1
    2
    3
    4
    5


### While loop

While loop can be used to execute a set of statements as long as a certain condition holds true.



```
i = 0

while i <=7:
    print(i)
    i = i + 1
```

    0
    1
    2
    3
    4
    5
    6
    7


### break() is used to exit a for loop or a while loop

### continue() is used to skip the current block, and return to the "for" or "while" statement.


```
# print out all elements in the list up until the Python (Ticker Symbol = Python) is detected
for i in my_list:
    print(i)
    if i == 'Python':
        break  
```

    GOOG
    [3, 6, 7]
    GOOG
    [3, 6, 7]
    GOOG
    [3, 6, 7]



```
# Print only odd elements and skip even numbers
No_list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

for i in No_list:
    if i%2 == 0:
        continue
    print(i)
```

    1
    3
    5
    7
    9


## List comprehension is an elegant tool to transform one list into another list. 

Instead of using loops and append, list comprehension is used to iterate over a list, condition its elements and include them in a new list.



```
input_list = [1, 2, 3, 4]

[ element ** 2  for element in input_list]
```




    [1, 4, 9, 16]



## Lambda function

Lambda function is used to create a function without a name 

Lambda functions are mainly used with filter() and map()

Lambda function can receive any number of arguments, but can only have one expression.


```
# We can do the same task using Lambda expression
# Note that there is no function name
y = lambda x:x**2
```

###  The map() function takes in a function and a list.

 map() performs an operation on the entire list and return the results in a new list.



```
# Define two lists a and b
a = [1, 4, 5, 6, 9]
b = [1, 7, 9, 12, 7]
```


```
# Let's define a function that adds two elements together
def summation(a, b):
    return a + b
```


```
# You can now use map() to apply a function to the entire list and generate a new list
c = list(map(summation, a, b))
c
```




    [2, 11, 14, 18, 16]



### filter is used to create a list of elements for which a function returns "True".



```
prices = [105, 5055, 40, 356, 923, 1443, 222, 62]
```


```
# return only even numbers
out = list(filter( lambda x: (x % 2 == 0) , prices  ))
out
```




    [40, 356, 222, 62]



## Files

- open() is the key function to handle files 
- open() function takes two parameters: (1) filename (2) mode.
- Modes for files opening: 

    - "r" - Read - Default value. Opens a file for reading, error if the file does not exist
    - "a" - Append - Opens a file for appending, creates the file if it does not exist
    - "w" - Write - Opens a file for writing, creates the file if it does not exist
    - "x" - Create - Creates the specified file, returns an error if the file exists

- files can be used in a binary or text mode

    - "t" - Text - Default value. Text mode
    - "b" - Binary - Binary mode (e.g. images)

f = open('sample_file.txt', 'r')

print(f.read())

outputs the content of sample file

### readline will be used to read the first line
print(f.readline())

### You can open the file and append content to it
f.write('this is a new line that I added to the file!')


### close the file and let's check its content
f.close()

