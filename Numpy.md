# Numpy

`import numpy as np`

`np.array()`
Create a NPA from a given list of lists
*Example*: `X = np.array([2**i for i in range(10)])`

`np.zeros(shape = (r, c))`
Create a matrix of dimensions r x c filled with 0

`np.ones(shape = (r, c))`
Create a matrix of dimensions r x c filled with 1

`np.linspace(start, stop, num)`
Create NPA with num equidistant elements starting in start and ending in stop

`x = x.reshape(r, c)`
NPAs can be reshaped into other NPAs:
*Note*: The product of the dimensions has to be the same before and after the reshape.
*Example*: We can reshape from (24) -> (3, 2, 4)

`X = X.T`
Transpose X

`np.concatenate([X_1, X_2], axis = 0)`
We can concatenate NPAs.
*Note*: The axis along which we concatenate has to be of the same dimension.

We can do arithmetic on NPAs as we can on scalar values. For two matrices X, Y we have
` X * Y` denotes the componentwise multiplication
`X.dot(Y)` denotes the classic matrix multiplication

### Math Operations
`np.exp(x)`
`np.log(x)`
`np.sin(x)`
`np.cos(x)`
`np.round(x, decimals = n)`

  

### Statistical methods:
`X.mean(axis)`
We can take the mean of a row (axis = 0) or a column (axis = 1)
`X.sum(axis)`
`X.std(axis)`
`X.min(axis)`
`X.max(axis)`
`X.argmin(axis)`
`X.argmax(axis)`

## Attributes of numpy arrays:

`X.shape`
gives the shape of X
*Example*: `np.zeros(shape = (r, c)).shape = (r, c)`

  np.unique(x)
  determines the unique modalities that appear in a sequence

### Conditional Slicing:
Conditions can be based on the values of the array:
`X[X < 0] = 0`
or on other numpy arrays:
`X[y == 1] = -1`

Iterating over numpy arrays:
1.  Rows
2.  Columns
3.  Channels

Example:
 - `for row in X:`
 - `for pixel in row:`
 - `for channel in pixel:`

 ### Broadcasting:
**Case 1**: Matrix and constant: The constant is broadcasted to the same dimension as the matrix and regular matrix addition is performed.
**Case 2**: Matrix and vector: This only works if for each dimension m of the matrix and v of the vector either: 

 - m = v or
 - m = 1 $\lor$ v = 1

*Example*:  `X = [[1, 2, 4], [2, 3, 5]] Y = [2, 3, 5]`
Then `X.shape = (2, 3)` and  `Y.shape = (1, 3)`

Y’s first dimension is equal to 1, and the second dimension of X and Y are equal. So broadcasting is possible.

X + Y will then be X + [Y, Y]
