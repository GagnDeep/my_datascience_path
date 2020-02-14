# Numpy

if started up using anaconda distribution

```
conda install numpy
```

else

```
pip install numpy
```

---

### Guide to revise

- For quick revision read the readme file
- For practical overview, go over these notebooks.
  - numpy arrays
  - numpy indexing and selection
  - numpy operations
  - numpy intro edx
- For little practical gain go over these notebooks
  - numpy-exersices
  - satellite image analysis

---

## Numpy Arrays: 

- these can be martices or vectors

- a list can be casted into an array which will provide a linear algebra api

- on top of that array

  ```
  import numpy as np
  
  array = np.array(list)
  ```

---

## API 

- np.arange(start_index, end_index, step_size)

  ​		this is similar to range in python 

  ​		it generate an array of values ranging from start index and end index

  ​		you can also provide a step size for evenly spaced values between that points

- np.zeros(size)

  ​		it provides a matrix of zeros according to the rank

  ​		size = single value for 1d matrix 

  ​		 		 or a tuple of values for multiple dimension

  ​		np.zeros((2,3)) // a matrix of 2 rows and 3 columns

- np.ones(size)

  ​		similar to np.zeros() but provides a matrix of 1's

- np.linspace(start, end, num)

  ​		- similar to np.arange() with step argument 

  ​		but arange provides array with that given step size

  ​		and linspace provide number of evenly space values

  ​		between that interval

- np.eye(num)

  ​		generates identity matrix of size <num>

  ​		takes a single argument because identity matrix is a square matrix

- np.random

  ​		import individual functions using import syntax

```
from np.random import randint
```



- np.random.rand(5, ...dimentions)

  ​			1d matrix of 5 random number from a uniform distribution between 0 and 1

- np.random.randn(1,2, ...dimentions)

  ​			2d matrix of size (1,2) having random values

  ​			it takes random numbers from a standard normal distribution centered

  ​			around 0 : gaussian distribution

- np.random.randint(low_inclusive, high_exclusive, size)

  ​			will provide a matrix of random integer values between the range

  ​			if not supplied any size value: will get a random int value between the range

​				`np.random.randint(1, 100, 10) //1 can be selected 100 cannot`

- arr.reshape(row, col)

  ​			this method can reshape an array to a new dimension

  ​			but the supplied array must have enough elements to fill up new shape

  ​				`np.arange(0,4).resape(2,2) // [[0,1],[2,3]]`

  ​				row*cols == number of actual elements

- np.random.seed(value)

  ​			it resets the seed to value passed such that same set of random numbers

  ​			will appear when random function will be called after reseting the seed

  ```
  np.random.seed(191)
  
  np.random.randn(10) // array of 10 random numbers
  
  np.random.seed(191)
  
  np.random.randn(10) // same array of 10 random numbers
  
  np.random.randn(10) // different array of 10 random number
  ```

  

---

## Some methods available on numpy arrays

- array.min() // returns min value of the matrix

- array.max() // returns max value of the matrix

- array.argmax() // returns the index of the max value of the matrix

- array.argmin() // returns the index of the min value of the matrix

- array.shape // will give you the shape of the matrix

- array.dtype // will give you the datatype of the matrix

---

## Indexing numpy arrays

- working with numpy arrays is similiar to how we worked with lists

  ```
  arr = np.arange(0,10)
  
  arr[1] // will give element on index 1
  ```

  

- slicing

  ```
  arr[1:5] // slice starting at index 1 and till index 5
  
  arr[:5] // from 0 to index 5
  
  arr[1:] // from index 1 till the last element
  
  arr[:] // all elements
  ```

  

- negative indexing

  ​		you can do negative indexing to get the last row

  ​		arr[-1] // will return the last element

- broadcasting 

  ​		numpy arrays differs from list in terms of broadcasting

  ​		numpy arrays have a feature know as broadcasting

  ​		a value can be broadcasted to selected or all elements by assigning 

## Rules for broadcasting

- When operating on two arrays, NumPy compares their shapes element-wise. It starts with the trailing dimensions, and works its way forward. Two dimensions are compatible when
  - They are equal 
  - or one of them is 1
  - more details https://docs.scipy.org/doc/numpy-1.10.1/user/basics.broadcasting.html

`numy_arr[0:7] = 100 //broadcast value 100 to elements 0:7`

`numpy_arr[:] = 100 //broadcast value 100 to all elements of array`

> this operation is mutable
>
> meaning that original array will be changed
>
> numpy doesnt create new arrays for each operation 
>
> instead it uses a refernce of old array

- array.copy()

​		this function is used to create copy of arrays to make things immutable

​			`copy = numpy_arr.copy()`

- double bracket notation

​		`array[1][2]`

- single bracket notation

​		`array[1,2]`

- you can also use slice notation while indexing 

​		arr[1:, 2:] //every row from index 1 onwards and col from index 2 onwards

​		arr[1:3, 2:4] // every row from index 1 to index 3, not including index 3

​					 // every col from index 2 to index 4, not including index 4

- conditional selection

  `arr = np.arange(1,10)`

   `bool_arr = arr > 3 // will return array with boolean values`

> in which element will be true where the value will be greater than 3

​		`arr[bool_arr] // will give the arr with elements only where the value`

> is true in the bool_arr

### the above two steps can be condensed into a single operation

`arr[arr > 3]`

---

## Array operations with numpy

- you can use all the basic operators with numpy arrays too

- such as multiplying with an array with array or scalar with a scalar

> using basic operators such as *, /, + , - ...

```
[1,2] \* [2,3] = [2,6]

[2, 3] \* 100 = [200, 300]
```

> operations performed doesn't mutate original array

**universal array operations**

> numpy comes with many universal array operations such as

- **np.sqrt(arr)** // square root of each element of the array

- **np.exp(arr)** // for exponential of the number

- **np.max(arr)** // returns the max valued element, similar to arr.max

- **np.sin(arr)** // sin of each number

- **np.log(arr)** // log of each function

>  if divide by zero of something like accur numpy will give you warning
>
> instead of
>
> zivide by zero in python gives you an error

​	

---

## From EDX

### Write numpy arrays to disk

- `np.save('filename', array)`
- `np.load('filename.npy)`
- save as text file
- np.savetxt('filename.txt', x=Array, delimiter=',')

**More operations**

- np.dot(x,y) or x.dot(y) 

  - #dot product

- array.T 

  - Transpose

- Indexing using where

  - np.where( mat > 0.5, 1000, -1) 
  - will provide an array with 1000 where conditon is true and -1 where false

- np.random.permutation(array) 

  - return new ordering for the array

- np.random.uniform(size=4)

  - uniform distribution

- np.random.normal(size=4)

- merging datasets

  - np.vstack((K,M)) 
  - np.concatenate([K, M.T], axis = 1) 
    
  - np.hstack((K, M)) 

    - np.concatenate([K, M], axis = 0)