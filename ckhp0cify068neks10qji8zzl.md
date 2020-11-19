## Peep into basics of Numpy and Pandas

This blog is written in Jupyter notebook, so you can experiment and learn by editing the notebook.   
Click  [here](https://github.com/kirankamatmgm/Interesting-Python/blob/main/refreshing_basics_of_Numpy_Pandas.ipynb)  for notebook.

Just change the input and check the output.

Learning by experiment and hands-on exercises is always better.

The purpose of this notebook is just to revise python basics.

Let's get started.

# 1. NUMPY BASICS

 NumPy is a Linear Algebra Library used for multidimensional arrays

 NumPy brings the best of two worlds: 
 - C/Fortran computational efficiency, 
 -  Python language easy syntax 


```
import numpy as np 

# Let's define a one-dimensional array 
my_list = [10, 20, 30, 40, 50, 60, 70, 80]
my_list
```




    [10, 20, 30, 40, 50, 60, 70, 80]



Let's create a numpy array from the list "my_list"


```
x = np.array(my_list)
x
```




    array([10, 20, 30, 40, 50, 60, 70, 80])


Get shape

```
x.shape
```




    (8,)



Let's create a Multi-dimensional numpy array from the list "my_list"

```

matrix = np.array([[5, 8], [9, 13]])
matrix
```




    array([[ 5,  8],
           [ 9, 13]])




```
# "rand()" uniform distribution between 0 and 1
xy = np.random.rand(7)
xy
```




    array([0.40408966, 0.12527144, 0.04465052, 0.39450693, 0.93339664,
           0.14009694, 0.94461679])



you can create a matrix of random number from random.rand

```

xy = np.random.rand(2, 2)
xy
```




    array([[0.86152202, 0.22526627],
           [0.41562272, 0.33467273]])




```
# "randn()" normal distribution between 0 and 1
xy = np.random.randn(7)
xy
```




    array([-1.27678101,  1.20667812,  0.7945132 ,  0.62421099, -0.44447512,
           -0.57038096,  2.19949273])


"randint" is used to generate random integers between upper and lower bounds

```

xy = np.random.randint(1, 10)
xy
```




    9



Create an evenly spaced values with a step of 7

```
xy = np.arange(1, 50, 7)
xy
```




    array([ 1,  8, 15, 22, 29, 36, 43])




```
# Array of ones
xy = np.ones(7)
xy
```




    array([1., 1., 1., 1., 1., 1., 1.])




```
# Matrices of ones
xy = np.ones((2, 2))
xy
```




    array([[1., 1.],
           [1., 1.]])




```
# Array of zeros
xy = np.zeros(5)
xy
```




    array([0., 0., 0., 0., 0.])



Reshape 1D array into a matrix

```
z = x.reshape(2,4)
print(x)
print(z)
```

    [10 20 30 40 50 60 70 80]
    [[10 20 30 40]
     [50 60 70 80]]


Obtain the maximum element (value)

```
x.max()
```




    80



Obtain the minimum element (value)

```
x.min()
```




    10



Obtain the location of the max element

```
x.argmax()
```




    7




```
# Obtain the location of the min element
x.argmin()
```




    0




```
# Access specific index from the numpy array
x[0]
```




    10




```
# Starting from the first index 0 up until and NOT including the last element
x[0:3]
```




    array([10, 20, 30])




```
# Broadcasting, altering several values in a numpy array at once
x[0:2] = 10
x
```




    array([10, 10, 30, 40, 50, 60, 70, 80])



# 2. Pandas

Pandas is a data manipulation and analysis tool that is built on Numpy.

Pandas uses a data structure known as DataFrame (think of it as Microsoft excel in Python). 

DataFrames empower programmers to store and manipulate data in a tabular fashion (rows and columns).

Series Vs. DataFrame? Series is considered a single column of a DataFrame.


```
import pandas as pd 
```


```
# Let's define two lists as shown below:
stock_list = ['Reliance','AMAZON','facebook']
stock_list

```




    ['Reliance', 'AMZN', 'facebook']




```
label   = ['stock#1', 'stock#2', 'stock#3']
label
```




    ['stock#1', 'stock#2', 'stock#3']



Let's create a one dimensional Pandas "series" 

Note that series is formed of data and associated labels
```
 
x_series = pd.Series(data = stock_list, index = label)
```


```
# Let's view the series
x_series
```




    stock#1    Reliance
    stock#2        AMZN
    stock#3    facebook
    dtype: object



Let's obtain the datatype

```
type(x_series)
```




    pandas.core.series.Series



Let's define a two-dimensional Pandas DataFrame

Note that you can create a pandas dataframe from a python dictionary
```

bank_client_df = pd.DataFrame({'Bank client ID':[1111, 2222, 3333, 4444], 
                               'Bank Client Name':['Kiran', 'Chaitanya', 'dheeraj', 'shreyas'], 
                               'Net worth [$]':[3500, 29000, 10000, 2000], 
                               'Years with bank':[3, 4, 9, 5]})
bank_client_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Bank client ID</th>
      <th>Bank Client Name</th>
      <th>Net worth [$]</th>
      <th>Years with bank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1111</td>
      <td>Kiran</td>
      <td>3500</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2222</td>
      <td>Chaitanya</td>
      <td>29000</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3333</td>
      <td>dheeraj</td>
      <td>10000</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4444</td>
      <td>shreyas</td>
      <td>2000</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



Let's obtain the data type 
```

type(bank_client_df)
```




    pandas.core.frame.DataFrame



you can only view the first couple of rows using .head()

```
bank_client_df.head(2)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Bank client ID</th>
      <th>Bank Client Name</th>
      <th>Net worth [$]</th>
      <th>Years with bank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1111</td>
      <td>Kiran</td>
      <td>3500</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2222</td>
      <td>Chaitanya</td>
      <td>29000</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>



you can only view the last couple of rows using .tail()

```
bank_client_df.tail(1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Bank client ID</th>
      <th>Bank Client Name</th>
      <th>Net worth [$]</th>
      <th>Years with bank</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>4444</td>
      <td>shreyas</td>
      <td>2000</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



### Pandas is used to read a csv file and store data in a DataFrame

bank_df = pd.read_csv('sample.csv')

### write to a csv file without an index

bank_df.to_csv('sample_output.csv', index = False)

## CONCATENATING AND MERGING WITH PANDAS


```
df1 = pd.DataFrame({'A': ['A0', 'A1', 'A2', 'A3'],
                    'B': ['B0', 'B1', 'B2', 'B3'],
                    'C': ['C0', 'C1', 'C2', 'C3'],
                    'D': ['D0', 'D1', 'D2', 'D3']},
index=[0, 1, 2, 3])
```


```
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
  </tbody>
</table>
</div>




```
df2 = pd.DataFrame({'A': ['A4', 'A5', 'A6', 'A7'],
                    'B': ['B4', 'B5', 'B6', 'B7'],
                    'C': ['C4', 'C5', 'C6', 'C7'],
                    'D': ['D4', 'D5', 'D6', 'D7']},
index=[4, 5, 6, 7]) 
```


```
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>A4</td>
      <td>B4</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>A5</td>
      <td>B5</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>A6</td>
      <td>B6</td>
      <td>C6</td>
      <td>D6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>A7</td>
      <td>B7</td>
      <td>C7</td>
      <td>D7</td>
    </tr>
  </tbody>
</table>
</div>




```
df3 = pd.DataFrame({'A': ['A8', 'A9', 'A10', 'A11'],
                    'B': ['B8', 'B9', 'B10', 'B11'],
                    'C': ['C8', 'C9', 'C10', 'C11'],
                    'D': ['D8', 'D9', 'D10', 'D11']},
index=[8, 9, 10, 11])
```


```
df3
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>8</th>
      <td>A8</td>
      <td>B8</td>
      <td>C8</td>
      <td>D8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>A9</td>
      <td>B9</td>
      <td>C9</td>
      <td>D9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>A10</td>
      <td>B10</td>
      <td>C10</td>
      <td>D10</td>
    </tr>
    <tr>
      <th>11</th>
      <td>A11</td>
      <td>B11</td>
      <td>C11</td>
      <td>D11</td>
    </tr>
  </tbody>
</table>
</div>




```
pd.concat([df1, df2, df3])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>A0</td>
      <td>B0</td>
      <td>C0</td>
      <td>D0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>A1</td>
      <td>B1</td>
      <td>C1</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>A2</td>
      <td>B2</td>
      <td>C2</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>A3</td>
      <td>B3</td>
      <td>C3</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>A4</td>
      <td>B4</td>
      <td>C4</td>
      <td>D4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>A5</td>
      <td>B5</td>
      <td>C5</td>
      <td>D5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>A6</td>
      <td>B6</td>
      <td>C6</td>
      <td>D6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>A7</td>
      <td>B7</td>
      <td>C7</td>
      <td>D7</td>
    </tr>
    <tr>
      <th>8</th>
      <td>A8</td>
      <td>B8</td>
      <td>C8</td>
      <td>D8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>A9</td>
      <td>B9</td>
      <td>C9</td>
      <td>D9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>A10</td>
      <td>B10</td>
      <td>C10</td>
      <td>D10</td>
    </tr>
    <tr>
      <th>11</th>
      <td>A11</td>
      <td>B11</td>
      <td>C11</td>
      <td>D11</td>
    </tr>
  </tbody>
</table>
</div>

