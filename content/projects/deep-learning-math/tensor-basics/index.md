---
title: 'Fundamentals of Tensors'
date: '2023-02-17'
summary: 'Understanding tensor dimensions from scalars to multi-dimensional arrays in PyTorch'
tags:
  - Deep Learning
  - PyTorch
  - Tensors
---

## Tensor Dimensions

### Zero-dimensional Tensor (Scalar)
A zero-dimensional tensor is a single number, also called a scalar.

### One-dimensional Tensor (Vector)
A one-dimensional tensor is a vector with only length and magnitude, represented as an array with no explicit rows or columns.

### Two-dimensional Tensor (Matrix)
A two-dimensional tensor has rows and columns, forming a matrix.

### Three-dimensional Tensor
A three-dimensional tensor has rows, columns, and depth. This is particularly useful for image processing, especially color images with RGB channels that require three dimensions for representation.

### Higher-dimensional Tensors
- **Four-dimensional tensor**: A collection of three-dimensional tensors
- **Five-dimensional tensor**: A four-dimensional tensor with additional row/column information
- **Six-dimensional tensor**: A five-dimensional tensor with additional depth information

## Understanding Tensor Structure

**Two-dimensional tensor**: A one-dimensional array where each element is a one-dimensional tensor

**Three-dimensional tensor**: A one-dimensional array where each element is a two-dimensional tensor

**Four-dimensional tensor**: A one-dimensional array where each element is a three-dimensional tensor

Tensors in PyTorch support GPU computation and automatic gradient calculation.

## PyTorch Tensor Examples

In PyTorch, the number of dimensions is determined by counting the number of brackets.

### Zero-dimensional Tensor
```python
tensor(1)  # Note: tensor([1]) is a one-dimensional tensor, not zero-dimensional
```

### One-dimensional Tensor
Length-3 one-dimensional tensor:
```python
tensor([0.8206, 0.6208, 0.2549])
```

### Two-dimensional Tensor
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

### Three-dimensional Tensor
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

## Terminology in Different Contexts

### Scalar
A scalar is a single number, also called a 0-dimensional array.

Example: The number "5" in "5 houses" is a scalar.

### Vector
A vector is a list of scalars, also called a 1-dimensional array.

Example: House price factors (school district, subway proximity, area, number of rooms, floor level) can be represented as a feature vector.

### Matrix
A matrix is a collection of vectors, also called a 2-dimensional array.

Example: If one house's features form a vector, then a dataset of m houses creates an m×n matrix (where n is the vector length).

### Tensor
A tensor is a generalization of matrices for N-dimensional data. In computer science, terminology is flexible: a matrix can be called a matrix, a 2nd-order tensor, or a 2-dimensional array.

## Tensors in Image Processing

Tensors are widely used in image processing:

**3D Tensor (Color Image)**: A color image has width, height, and three channels (R, G, B), forming a 3rd-order tensor.

**4D Tensor (Batch of Images)**: During training or inference in image recognition, we process N images at once. This batch dimension creates a 4th-order tensor with dimensions: `batch_size × channels × width × height`.
