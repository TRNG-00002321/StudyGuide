# NumPy

## What is NumPy?
NumPy is a Python library used for working with arrays.
It also has functions for working in domain of linear algebra, fourier transform, and matrices.
NumPy was created in 2005 by Travis Oliphant. It is an open source project and you can use it freely.
NumPy stands for Numerical Python.

## Why Use NumPy?
NumPy aims to provide an array object that is up to 50x faster than traditional Python lists.
The array object in NumPy is called ndarray, it provides a lot of supporting functions that make working with ndarray very easy.
Arrays are very frequently used in data science, where speed and resources are very important.

## Installation of NumPy
`pip install numpy`

## Import NumPy
Once NumPy is installed, import it in your applications by adding the import keyword<br/>
`import numpy`

## Create a NumPy ndarray Object
NumPy is used to work with arrays. The array object in NumPy is called ndarray.
We can create a NumPy ndarray object by using the array() function.

```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5])
print(arr)
print(type(arr))

# OUTPUT
[1 2 3 4 5]
<class 'numpy.ndarray'>
```

## Dimensions in Arrays
A dimension in arrays is one level of array depth (nested arrays).  
**0-D Arrays**  
0-D arrays, or Scalars, are the elements in an array. Each value in an array is a 0-D array.
```python
import numpy as np
arr = np.array(42)
print(arr)
```  
**1-D Arrays**  
An array that has 0-D arrays as its elements is called uni-dimensional or 1-D array.  
These are the most common and basic arrays.  
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5])
print(arr)
```  
**2-D Arrays**  
An array that has 1-D arrays as its elements is called a 2-D array.
These are often used to represent matrix or 2nd order tensors.
```python
import numpy as np
arr = np.array([[1, 2, 3], [4, 5, 6]])
print(arr)
```

**Check Number of Dimensions?**  
NumPy Arrays provides the `ndim` attribute that returns an integer that tells us how many dimensions the array have.
```python
import numpy as np

a = np.array(42)
b = np.array([1, 2, 3, 4, 5])
c = np.array([[1, 2, 3], [4, 5, 6]])
d = np.array([[[1, 2, 3], [4, 5, 6]], [[1, 2, 3], [4, 5, 6]]])

print(a.ndim)
print(b.ndim)
print(c.ndim)
print(d.ndim)
```

**Higher Dimensional Arrays**  
An array can have any number of dimensions.
When the array is created, you can define the number of dimensions by using the ndmin argument.
```python
import numpy as np

arr = np.array([1, 2, 3, 4], ndmin=5)
print(arr)
print('number of dimensions :', arr.ndim)
```

## NumPy Array Indexing

**Access Array Elements**  
Array indexing is the same as accessing an array element.
You can access an array element by referring to its index number.
The indexes in NumPy arrays start with 0, meaning that the first element has index 0, and the second has index 1 etc.

```python
import numpy as np
arr = np.array([1, 2, 3, 4])
print(arr[0])
```

**Access 2-D Arrays**  
To access elements from 2-D arrays we can use comma separated integers representing the dimension and the index of the element.
Think of 2-D arrays like a table with rows and columns, where the dimension represents the row and the index represents the column.

_Access the element on the 2nd row, 5th column:_
```python
import numpy as np
arr = np.array([[1,2,3,4,5], [6,7,8,9,10]])
print('5th element on 2nd row: ', arr[1, 4])
```

**Access 3-D Arrays**  
To access elements from 3-D arrays we can use comma separated integers representing the dimensions and the index of the element.

_Access the third element of the second array of the first array:_
```python
import numpy as np
arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])
print(arr[0, 1, 2])

# OUTPUT
arr[0, 1, 2] prints the value 6.
```

**Negative Indexing**  
Use negative indexing to access an array from the end.

_Print the last element from the 2nd dim:_
```pyt_hon
import numpy as np
arr = np.array([[1,2,3,4,5], [6,7,8,9,10]])
print('Last element from 2nd dim: ', arr[1, -1])
```

## NumPy Array Slicing

**Slicing arrays**  
Slicing in python means taking elements from one given index to another given index.
We pass slice instead of index like this: `[start:end]`.
We can also define the step, like this: `[start:end:step]`.
If we don't pass start its considered 0
If we don't pass end its considered length of array in that dimension
If we don't pass step its considered 1

_Slice elements from index 1 to index 5 from the following array:_
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[1:5])
```
**Note: The result includes the start index, but excludes the end index.**
#### Other Examples
- **`Slice elements from index 4 to the end of the array: print(arr[4:])`**
- **`Slice elements from the beginning to index 4 (not included): print(arr[:4])`**

**Negative Slicing**  
Use the minus operator to refer to an index from the end:
Slice from the index 3 from the end to index 1 from the end:
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[-3:-1])
```

**STEP**  
Use the step value to determine the step of the slicing:

_Return every other element from index 1 to index 5:_
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[1:5:2])
```

**Slicing 2-D Arrays**  
_From the second element, slice elements from index 1 to index 4 (not included):_
```python
import numpy as np
arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[1, 1:4])
```

### NumPy Data Types  
NumPy has some extra data types, and refer to data types with one character, like i for integers, u for unsigned integers etc.  
Below is a list of all data types in NumPy and the characters used to represent them.
- i - integer
- b - boolean
- u - unsigned integer
- f - float
- c - complex float
- m - timedelta
- M - datetime
- O - object
- S - string
- U - unicode string
- V - fixed chunk of memory for other type ( void )

**Checking the Data Type of an Array**  
The NumPy array object has a property called dtype that returns the data type of the array:
_Get the data type of an array object:_
```python
import numpy as np
arr = np.array([1, 2, 3, 4])
print(arr.dtype)
```

**Creating Arrays With a Defined Data Type**  
We use the array() function to create arrays, this function can take an optional argument: dtype that allows us to define the expected data type of the array elements:
_Create an array with data type string:_
```python
import numpy as np
arr = np.array([1, 2, 3, 4], dtype='S')
print(arr)
print(arr.dtype)
```
**Note : For i, u, f, S and U we can define size as well.**

## NumPy Array Shape & Reshaping
**Shape of an Array**    
The shape of an array is the number of elements in each dimension.

**Get the Shape of an Array**  
NumPy arrays have an attribute called `shape` that returns a tuple with each index having the number of corresponding elements.  
_Print the shape of a 2-D array:_
```python
import numpy as np
arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
print(arr.shape)

#OUTPUT 
(2, 4)
```

**Reshaping arrays**  
Reshaping means changing the shape of an array.
The shape of an array is the number of elements in each dimension.
By reshaping we can add or remove dimensions or change number of elements in each dimension.

**Reshape From 1-D to 2-D**  
Convert the following 1-D array with 12 elements into a 2-D array.
The outermost dimension will have 4 arrays, each with 3 elements:
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12])
newarr = arr.reshape(4, 3)
print(newarr)

# OUTPUT
[[ 1  2  3]
 [ 4  5  6]
 [ 7  8  9]
 [10 11 12]]
```
**Reshape From 1-D to 3-D**  
Convert the following 1-D array with 12 elements into a 3-D array.
The outermost dimension will have 2 arrays that contains 3 arrays, each with 2 elements:
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12])
newarr = arr.reshape(2, 3, 2)
print(newarr)

# OUTPUT
[[[ 1  2]
  [ 3  4]
  [ 5  6]]

 [[ 7  8]
  [ 9 10]
  [11 12]]]
```

**Flattening the arrays**  
Flattening array means converting a multidimensional array into a 1D array.
We can use reshape(-1) to do this.

_Convert the array into a 1D array:_  
```python
import numpy as np
arr = np.array([[1, 2, 3], [4, 5, 6]])
newarr = arr.reshape(-1)
print(newarr)

# OUTPUT
[1 2 3 4 5 6]
```

## NumPy Array Iterating  
Iterating means going through elements one by one.
As we deal with multi-dimensional arrays in numpy, we can do this using basic for loop of python.
If we iterate on a 1-D array it will go through each element one by one.

_Iterate on the elements of the following 1-D array:_  
```python
import numpy as np
arr = np.array([1, 2, 3])
for x in arr:
  print(x)
  ```

**Iterating 3-D Arrays**  
```python
import numpy as np

arr = np.array([[[1, 2, 3], [4, 5, 6]], [[7, 8, 9], [10, 11, 12]]])

for x in arr:
  for y in x:
    for z in y:
      print(z)
```

**Iterating Arrays Using nditer()**  
The function `nditer()` is a helping function that can be used from very basic to very advanced iterations. It solves some basic issues which we face in iteration.

**Iterating on Each Scalar Element**  
In basic for loops, iterating through each scalar of an array we need to use n for loops which can be difficult to write for arrays with very high dimensionality.

```python
import numpy as np
arr = np.array([[[1, 2], [3, 4]], [[5, 6], [7, 8]]])
for x in np.nditer(arr):
  print(x)
```

**Iterate through every scalar element of the 2D array skipping 1 element:**  
```python
import numpy as np
arr = np.array([[1, 2, 3, 4], [5, 6, 7, 8]])
for x in np.nditer(arr[:, ::2]):
  print(x)
```

## NumPy Joining Array
**Joining NumPy Arrays**  
Joining means putting contents of two or more arrays in a single array.
In SQL we join tables based on a key, whereas in NumPy we join arrays by axes.
We pass a sequence of arrays that we want to join to the concatenate() function, along with the axis. If axis is not explicitly passed, it is taken as 0.

_Join two arrays_  
```python
import numpy as np
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
arr = np.concatenate((arr1, arr2))
print(arr)
```

_Join two 2-D arrays along rows (axis=1):_
```python
import numpy as np
arr1 = np.array([[1, 2], [3, 4]])
arr2 = np.array([[5, 6], [7, 8]])
arr = np.concatenate((arr1, arr2), axis=1)
print(arr)
```

**Joining Arrays Using Stack Functions**   
Stacking is same as concatenation, the only difference is that stacking is done along a new axis.
We can concatenate two 1-D arrays along the second axis which would result in putting them one over the other, ie. stacking.
We pass a sequence of arrays that we want to join to the stack() method along with the axis. If axis is not explicitly passed it is taken as 0.

```python
import numpy as np
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
arr = np.stack((arr1, arr2), axis=1)
print(arr)
```

**Stacking Along Rows**  
NumPy provides a helper function: hstack() to stack along rows.
```python
import numpy as np
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
arr = np.hstack((arr1, arr2))
print(arr)
```

**Stacking Along Columns**  
NumPy provides a helper function: vstack()  to stack along columns.
```python
import numpy as np
arr1 = np.array([1, 2, 3])
arr2 = np.array([4, 5, 6])
arr = np.vstack((arr1, arr2))
print(arr)
```

## NumPy Splitting Array  
Splitting is reverse operation of Joining.
Joining merges multiple arrays into one and Splitting breaks one array into multiple.
We use `array_split()` for splitting arrays, we pass it the array we want to split and the number of splits.  
_Split the array in 3 parts:_  
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6])
newarr = np.array_split(arr, 3)
print(newarr)
```
**`Note:`** `The return value is a list containing three arrays.`

**You can also use hsplit(), vsplit() as well**

## NumPy Searching Arrays
You can search an array for a certain value, and return the indexes that get a match.
To search an array, use the `where()` method.

_Find the indexes where the value is 4:_
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 4, 4])
x = np.where(arr == 4)
print(x)

#OUTPUT
The example above will return a tuple: (array([3, 5, 6],)
Which means that the value 4 is present at index 3, 5, and 6.
```

**Search Sorted**  
There is a method called `searchsorted()` which performs a binary search in the array, and returns the index where the specified value would be inserted to maintain the search order.
The `searchsorted()` method is assumed to be used on sorted arrays.

_Find the indexes where the value 7 should be inserted:_
```python
import numpy as np
arr = np.array([6, 7, 8, 9])
x = np.searchsorted(arr, 7)
print(x)
```

**Search From the Right Side**  
By default the left most index is returned, but we can give side='right' to return the right most index instead.

_Find the indexes where the value 7 should be inserted, starting from the right:_
```python
import numpy as np
arr = np.array([6, 7, 8, 9])
x = np.searchsorted(arr, 7, side='right')
print(x)
```

## NumPy Sorting Arrays  
Sorting means putting elements in an ordered sequence.
Ordered sequence is any sequence that has an order corresponding to elements, like numeric or alphabetical, ascending or descending.
The NumPy ndarray object has a function called sort(), that will sort a specified array.  
_Sort the array:_
```python
import numpy as np
arr = np.array([3, 2, 0, 1])
print(np.sort(arr))
```
**Note: This method returns a copy of the array, leaving the original array unchanged.**

**Sorting a 2-D Array**  
If you use the sort() method on a 2-D array, both arrays will be sorted:  
_Sort a 2-D array:_
```python
import numpy as np
arr = np.array([[3, 2, 4], [5, 0, 1]])
print(np.sort(arr))
```

## NumPy Filter Array  
Getting some elements out of an existing array and creating a new array out of them is called filtering.
In NumPy, you filter an array using a boolean index list.
A boolean index list is a list of booleans corresponding to indexes in the array.
If the value at an index is True that element is contained in the filtered array, if the value at that index is False that element is excluded from the filtered array.

_Create an array from the elements on index 0 and 2:_
```python
import numpy as np
arr = np.array([41, 42, 43, 44])
x = [True, False, True, False]
newarr = arr[x]
print(newarr)
```
  
_Create a filter array that will return only values higher than 42:_
```python
import numpy as np

arr = np.array([41, 42, 43, 44])

# Create an empty list
filter_arr = []

# go through each element in arr
for element in arr:
  # if the element is higher than 42, set the value to True, otherwise False:
  if element > 42:
    filter_arr.append(True)
  else:
    filter_arr.append(False)

newarr = arr[filter_arr]

print(filter_arr)
print(newarr)
```

_Create a filter array that will return only even elements from the original array:_
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5, 6, 7])
filter_arr = arr % 2 == 0
newarr = arr[filter_arr]
print(filter_arr)
print(newarr)
```