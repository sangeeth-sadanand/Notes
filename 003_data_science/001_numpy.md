## Import Numpy package

```python
import numpy as np
```

## Create np vector from list

```python
list_ = [1,2,3]
arr = np.array(list_)
arr
```

    array([1, 2, 3])

```python
matrix = [[1,2,3],[4,5,6],[7,8,9]]
arr1 = np.array(matrix)
arr1
```

    array([[1, 2, 3],
           [4, 5, 6],
           [7, 8, 9]])

```python
np.arange(1,10)
```

    array([1, 2, 3, 4, 5, 6, 7, 8, 9])

```python
np.zeros(3)
```

    array([0., 0., 0.])

```python
np.zeros((3,2,2))
```

    array([[[0., 0.],
            [0., 0.]],
    
           [[0., 0.],
            [0., 0.]],
    
           [[0., 0.],
            [0., 0.]]])

```python
np.ones(2)
```

    array([1., 1.])

```python
np.ones((2,3))
```

    array([[1., 1., 1.],
           [1., 1., 1.]])

```python
np.linspace(0,4,10)
```

    array([0.        , 0.44444444, 0.88888889, 1.33333333, 1.77777778,
           2.22222222, 2.66666667, 3.11111111, 3.55555556, 4.        ])

```python
np.eye(4)
```

    array([[1., 0., 0., 0.],
           [0., 1., 0., 0.],
           [0., 0., 1., 0.],
           [0., 0., 0., 1.]])

```python
np.random.rand(2,2)
```

    array([[0.85438002, 0.47529486],
           [0.60647459, 0.31729569]])

```python
np.random.randn(2,2)
```

    array([[-0.21939017, -0.88118577],
           [-1.19947096,  0.04250486]])

```python
np.random.randint(1,100,(10,2))
```

    array([[28, 16],
           [24, 46],
           [72, 55],
           [36,  5],
           [70, 28],
           [26, 65],
           [ 1, 15],
           [82, 21],
           [65, 89],
           [68, 25]], dtype=int32)

## Reshape

```python
arr = np.random.randint(1,100,9)
arr.reshape(3,3)
```

    array([[77, 76, 67],
           [11, 19, 44],
           [50, 24, 19]], dtype=int32)

## Some functions

```python
arr.max()
```

    np.int32(77)

```python
arr.min()
```

    np.int32(11)

```python
arr.argmin()
```

    np.int64(3)

```python
arr.argmax()
```

    np.int64(0)

```python
arr.shape
```

    (9,)

```python
arr.dtype
```

    dtype('int32')

## Indexing

1. **Basic Indexing**: Similar to Python lists, you can use square brackets to access elements in an array.

```python
arr = np.array([1, 2, 3, 4, 5])
print(arr[0])  # Output: 1
print(arr[-1]) # Output: 5
```

    1
    5

2. **Slicing**: You can use slicing to access a range of elements.

```python
arr = np.array([1, 2, 3, 4, 5])
print(arr[1:4])  # Output: [2 3 4]
```

    [2 3 4]

3. **Boolean Indexing**: You can use boolean conditions to filter elements.

```python
arr = np.array([1, 2, 3, 4, 5])
print(arr[arr > 2])  # Output: [3 4 5]
```

    [3 4 5]

4. **Fancy Indexing**: You can use arrays of indices to access specific elements.

```python
arr = np.array([1, 2, 3, 4, 5])
indices = [0, 2, 4]
print(arr[indices])  # Output: [1 3 5]
```

    [1 3 5]

5. **Multidimensional Indexing**: You can index into multi-dimensional arrays using a tuple of indices.

```python
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])
print(arr[1, 2])  # Output: 6
```

    6

## Operators

1. **Arithmetic Operators**:
   - Addition (`+`): Adds corresponding elements.

```python
 import numpy as np
 a = np.array([1, 2, 3])
 b = np.array([4, 5, 6])
 print(a + b)  # Output: [5 7 9]
```

    [5 7 9]

- Subtraction (`-`): Subtracts corresponding elements.

```python
print(a - b)  # Output: [-3 -3 -3]
```

    [-3 -3 -3]

- Multiplication (`*`): Multiplies corresponding elements.

```python
print(a * b)  # Output: [4 10 18]
```

    [ 4 10 18]

- Division (`/`): Divides corresponding elements. 

```python
print(a / b)  # Output: [0.25 0.4  0.5]
```

    [0.25 0.4  0.5 ]

- Modulus (`%`): Computes the remainder of division.

```python
print(a % b)  # Output: [1 2 3]
```

    [1 2 3]

2. **Comparison Operators**:
   
   - Greater than (`>`): Checks if elements of one array are greater than the corresponding elements of another array.

```python
print(a > b)  # Output: [False False False]
```

    [False False False]

- Less than (`<`): Checks if elements of one array are less than the corresponding elements of another array.

```python
print(a < b)  # Output: [ True  True  True]
```

    [ True  True  True]

- Equal to (`==`): Checks if elements of one array are equal to the corresponding elements of another array.

```python
print(a == b)  # Output: [False False False]
```

    [False False False]

- Not equal to (`!=`): Checks if elements of one array are not equal to the corresponding elements of another array.

```python
print(a != b)  # Output: [ True  True  True]
```

    [ True  True  True]

3. **Logical Operators**:
   - Logical AND (`&`): Performs element-wise logical AND.

```python
 c = np.array([True, False, True])
 d = np.array([False, False, True])
 print(c & d)  # Output: [False False  True]
```

    [False False  True]

- Logical OR (`|`): Performs element-wise logical OR.

```python
print(c | d)  # Output: [ True False  True]
```

    [ True False  True]

- Logical NOT (`~`): Inverts the boolean value of each element.

```python
print(~c)  # Output: [False  True False]
```

    [False  True False]

4. **Dot Product**: Computes the dot product of two arrays.

```python
print(np.dot(a, b))  # Output: 32 (which is 1*4 + 2*5 + 3*6)
```

    32

5. **Matrix Multiplication**: Performs matrix multiplication using the `@` operator or `np.matmul`.

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])
print(A @ B)  # Output: [[19 22]
             #          [43 50]]
```

    [[19 22]
     [43 50]]
