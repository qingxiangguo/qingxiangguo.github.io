---
title: '1.3 Tensor Attributes'
date: '2025-01-17'
summary: 'Understanding tensor properties: shape, data type, and device location'
tags:
  - Deep Learning
  - PyTorch
  - Tensors
---

Tensor attributes include shape, data type, and storage device location (CPU or GPU).

## Examining Tensor Attributes

```python
import torch

tensor = torch.rand(3, 4)  # Create a 3×4 2D tensor

print(f"Shape of tensor: {tensor.shape}")
print(f"Datatype of tensor: {tensor.dtype}")
print(f"Device tensor is stored on: {tensor.device}")
```

## Output and Explanation

```
Shape of tensor: torch.Size([3, 4])
Datatype of tensor: torch.float32
Device tensor is stored on: cpu
```

### Shape
`tensor.shape` returns the dimensions of the tensor. In this example, `torch.Size([3, 4])` indicates a 2D tensor with 3 rows and 4 columns.

### Data Type
`tensor.dtype` returns the data type of the tensor elements. Common PyTorch data types include:
- `torch.float32` (default for floating-point)
- `torch.int64` (for integers)
- `torch.bool` (for boolean values)

### Device
`tensor.device` indicates where the tensor is stored:
- `cpu`: Stored in CPU memory
- `cuda:0`: Stored on GPU (first GPU device)

## Moving Tensors Between Devices

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
