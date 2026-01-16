---
title: 'Chapter 1: Tensors and Tensor Operations'
date: '2025-01-17'
summary: 'Understanding tensors: fundamentals, creation, attributes, and operations in PyTorch'
tags:
  - Deep Learning
  - PyTorch
  - Tensors
---

## 1.1 Fundamentals of Tensors

### Tensor Dimensions

#### Zero-dimensional Tensor (Scalar)
A zero-dimensional tensor is a single number, also called a scalar.

#### One-dimensional Tensor (Vector)
A one-dimensional tensor is a vector with only length and magnitude, represented as an array with no explicit rows or columns.

#### Two-dimensional Tensor (Matrix)
A two-dimensional tensor has rows and columns, forming a matrix.

#### Three-dimensional Tensor
A three-dimensional tensor has rows, columns, and depth. This is particularly useful for image processing, especially color images with RGB channels that require three dimensions for representation.

#### Higher-dimensional Tensors
- **Four-dimensional tensor**: A collection of three-dimensional tensors
- **Five-dimensional tensor**: A four-dimensional tensor with additional row/column information
- **Six-dimensional tensor**: A five-dimensional tensor with additional depth information

### Understanding Tensor Structure

**Two-dimensional tensor**: A one-dimensional array where each element is a one-dimensional tensor

**Three-dimensional tensor**: A one-dimensional array where each element is a two-dimensional tensor

**Four-dimensional tensor**: A one-dimensional array where each element is a three-dimensional tensor

Tensors in PyTorch support GPU computation and automatic gradient calculation.

### PyTorch Tensor Examples

In PyTorch, the number of dimensions is determined by counting the number of brackets.

#### Zero-dimensional Tensor
```python
tensor(1)  # Note: tensor([1]) is a one-dimensional tensor, not zero-dimensional
```

#### One-dimensional Tensor
Length-3 one-dimensional tensor:
```python
tensor([0.8206, 0.6208, 0.2549])
```

#### Two-dimensional Tensor
A 4×4 matrix:
```python
tensor([[1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]])
```

A 2×3 tensor:
```python
tensor([[0.9667, 0.8103, 0.6089],
        [0.5163, 0.8044, 0.7744]])
```

#### Three-dimensional Tensor
Two 2×3 matrices forming a 3D tensor:
```python
tensor([[[0.8929, 0.0102, 0.2182],
         [0.4855, 0.0377, 0.8328]],

        [[0.4653, 0.6590, 0.4474],
         [0.6367, 0.2073, 0.6972]]])
```

This is equivalent to:
```python
a1 = np.array([[0.8929, 0.0102, 0.2182], [0.4855, 0.0377, 0.8328]])
a2 = np.array([[0.4653, 0.6590, 0.4474], [0.6367, 0.2073, 0.6972]])
t3 = torch.tensor([a1, a2])
t3.shape  # Output: torch.Size([2, 2, 3])
```

### Terminology in Different Contexts

#### Scalar
A scalar is a single number, also called a 0-dimensional array.

Example: The number "5" in "5 houses" is a scalar.

#### Vector
A vector is a list of scalars, also called a 1-dimensional array.

Example: House price factors (school district, subway proximity, area, number of rooms, floor level) can be represented as a feature vector.

#### Matrix
A matrix is a collection of vectors, also called a 2-dimensional array.

Example: If one house's features form a vector, then a dataset of m houses creates an m×n matrix (where n is the vector length).

#### Tensor
A tensor is a generalization of matrices for N-dimensional data. In computer science, terminology is flexible: a matrix can be called a matrix, a 2nd-order tensor, or a 2-dimensional array.

### Tensors in Image Processing

Tensors are widely used in image processing:

**3D Tensor (Color Image)**: A color image has width, height, and three channels (R, G, B), forming a 3rd-order tensor.

**4D Tensor (Batch of Images)**: During training or inference in image recognition, we process N images at once. This batch dimension creates a 4th-order tensor with dimensions: `batch_size × channels × width × height`.

---

## 1.2 Creating Tensors in PyTorch

Tensors can be created directly from data, with data types automatically inferred.

### Creating Tensors from Data

```python
import torch
import numpy as np

data = [[1, 2], [3, 4]]
x_data = torch.tensor(data)  # Create tensor directly from data
```

### Creating Tensors from NumPy Arrays

```python
np_array = np.array(data)
x_np = torch.from_numpy(np_array)
```

### Creating Tensors with Similar Properties

Unless explicitly overridden, new tensors retain the properties (shape, datatype) of the original tensor.

#### Using `ones_like()`

The `ones_like()` method generates a tensor with the same shape as the input, filled with ones.

```python
x_ones = torch.ones_like(x_data)  # retains the properties of x_data
print(f"Ones Tensor: \n {x_ones} \n")
```

**Output:**
```
Ones Tensor:   # A 2D tensor (matrix)
 tensor([[1, 1],
        [1, 1]]) 
```

#### Using `rand_like()` with Type Override

```python
x_rand = torch.rand_like(x_data, dtype=torch.float)  # Override x_data's datatype to float
print(f"Random Tensor: \n {x_rand} \n")
```

The `rand_like()` method returns a tensor of the same size as the input, filled with random numbers from a uniform distribution over the interval [0, 1).

**Output:**
```
Random Tensor: 
 tensor([[0.4815, 0.7297],
        [0.8659, 0.5418]]) 
```

### Creating Tensors with Shape Parameters

You can also generate arrays of specified shapes using shape parameters.

```python
shape = (2, 5)
rand_tensor = torch.rand(shape)    # Generate a 2×5 2D tensor
ones_tensor = torch.ones(shape)
zeros_tensor = torch.zeros(shape)

print(f"Random Tensor: \n {rand_tensor} \n")
print(f"Ones Tensor: \n {ones_tensor} \n")
print(f"Zeros Tensor: \n {zeros_tensor}")
```

**Output:**
```
Random Tensor: 
 tensor([[0.1508, 0.6889, 0.6048, 0.5894, 0.7655],
        [0.2653, 0.7928, 0.1190, 0.3876, 0.1684]]) 

Ones Tensor: 
 tensor([[1., 1., 1., 1., 1.],
        [1., 1., 1., 1., 1.]]) 

Zeros Tensor: 
 tensor([[0., 0., 0., 0., 0.],
        [0., 0., 0., 0., 0.]])
```

### Summary of Creation Methods

PyTorch provides flexible methods for tensor creation:
- **From data**: `torch.tensor(data)`
- **From NumPy**: `torch.from_numpy(array)`
- **With same shape**: `ones_like()`, `rand_like()`
- **With specific shape**: `torch.rand()`, `torch.ones()`, `torch.zeros()`

---

## 1.3 Tensor Attributes

Tensor attributes include shape, data type, and storage device location (CPU or GPU).

### Examining Tensor Attributes

```python
import torch

tensor = torch.rand(3, 4)  # Create a 3×4 2D tensor

print(f"Shape of tensor: {tensor.shape}")
print(f"Datatype of tensor: {tensor.dtype}")
print(f"Device tensor is stored on: {tensor.device}")
```

### Output and Explanation

```
Shape of tensor: torch.Size([3, 4])
Datatype of tensor: torch.float32
Device tensor is stored on: cpu
```

#### Shape
`tensor.shape` returns the dimensions of the tensor. In this example, `torch.Size([3, 4])` indicates a 2D tensor with 3 rows and 4 columns.

#### Data Type
`tensor.dtype` returns the data type of the tensor elements. Common PyTorch data types include:
- `torch.float32` (default for floating-point)
- `torch.int64` (for integers)
- `torch.bool` (for boolean values)

#### Device
`tensor.device` indicates where the tensor is stored:
- `cpu`: Stored in CPU memory
- `cuda:0`: Stored on GPU (first GPU device)

### Moving Tensors Between Devices

You can move tensors to GPU for faster computation:

```python
# Move to GPU if available
if torch.cuda.is_available():
    tensor = tensor.to('cuda')
    print(f"Device tensor is stored on: {tensor.device}")
```

Understanding these attributes is crucial for:
- Managing memory efficiently
- Ensuring compatible operations between tensors
- Optimizing computation with GPU acceleration
