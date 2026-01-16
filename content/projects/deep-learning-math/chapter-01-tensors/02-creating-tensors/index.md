---
title: '1.2 Creating Tensors in PyTorch'
date: '2025-01-17'
summary: 'Different methods to create tensors from data, NumPy arrays, and using shape parameters'
tags:
  - Deep Learning
  - PyTorch
  - Tensors
---

Tensors can be created directly from data, with data types automatically inferred.

## Creating Tensors from Data

```python
import torch
import numpy as np

data = [[1, 2], [3, 4]]
x_data = torch.tensor(data)  # Create tensor directly from data
```

## Creating Tensors from NumPy Arrays

```python
np_array = np.array(data)
x_np = torch.from_numpy(np_array)
```

## Creating Tensors with Similar Properties

Unless explicitly overridden, new tensors retain the properties (shape, datatype) of the original tensor.

### Using `ones_like()`

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

### Using `rand_like()` with Type Override

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

## Creating Tensors with Shape Parameters

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

## Summary

PyTorch provides flexible methods for tensor creation:
- **From data**: `torch.tensor(data)`
- **From NumPy**: `torch.from_numpy(array)`
- **With same shape**: `ones_like()`, `rand_like()`
- **With specific shape**: `torch.rand()`, `torch.ones()`, `torch.zeros()`
