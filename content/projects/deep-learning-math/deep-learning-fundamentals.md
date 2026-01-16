---
title: 'Deep Learning Fundamentals'
date: '2025-01-17'
summary: 'Comprehensive guide to tensors, derivatives, and mathematical foundations of deep learning'
tags:
  - Deep Learning
  - PyTorch
  - Calculus
  - Mathematics
---

# Chapter 1: Tensors and Tensor Operations

## 1.1 Fundamentals of Tensors

**Zero-dimensional Tensor (Scalar)**: A single number, also called a scalar.

**One-dimensional Tensor (Vector)**: A vector with only length and magnitude, represented as an array.

**Two-dimensional Tensor (Matrix)**: Has rows and columns, forming a matrix.

**Three-dimensional Tensor**: Has rows, columns, and depth. Particularly useful for color images with RGB channels.

**Higher-dimensional Tensors**: Four-dimensional tensors are collections of 3D tensors, five-dimensional tensors add row/column information, and so on.

**Key concept**: An n-dimensional tensor is a one-dimensional array where each element is an (n-1)-dimensional tensor.

Tensors in PyTorch support GPU computation and automatic gradient calculation.

**Counting dimensions in PyTorch**: Count the number of brackets. For example, `tensor(1)` is zero-dimensional, while `tensor([1])` is one-dimensional.

**Examples:**

```python
# One-dimensional tensor (length 3)
tensor([0.8206, 0.6208, 0.2549])

# Two-dimensional tensor (4×4 matrix)
tensor([[1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.],
        [1., 1., 1., 1.]])

# Three-dimensional tensor (two 2×3 matrices)
tensor([[[0.8929, 0.0102, 0.2182],
         [0.4855, 0.0377, 0.8328]],
        [[0.4653, 0.6590, 0.4474],
         [0.6367, 0.2073, 0.6972]]])
```

The 3D tensor above is equivalent to:
```python
a1 = np.array([[0.8929, 0.0102, 0.2182], [0.4855, 0.0377, 0.8328]])
a2 = np.array([[0.4653, 0.6590, 0.4474], [0.6367, 0.2073, 0.6972]])
t3 = torch.tensor([a1, a2])
t3.shape  # Output: torch.Size([2, 2, 3])
```

**Terminology**: 
- **Scalar**: A single number (0D array). Example: "5" in "5 houses"
- **Vector**: A list of scalars (1D array). Example: house features like [area, rooms, floor]
- **Matrix**: A collection of vectors (2D array). Example: m houses with n features each
- **Tensor**: Generalization of matrices to N dimensions

**Tensors in image processing**:
- **3D Tensor**: Color image with dimensions width × height × channels (RGB)
- **4D Tensor**: Batch of images with dimensions batch_size × channels × width × height

---

## 1.2 Creating Tensors in PyTorch

Tensors can be created directly from data with automatic type inference:

```python
import torch
import numpy as np

# From Python lists
data = [[1, 2], [3, 4]]
x_data = torch.tensor(data)

# From NumPy arrays
np_array = np.array(data)
x_np = torch.from_numpy(np_array)
```

**Creating tensors with similar properties** - new tensors retain the shape and datatype unless overridden:

```python
# Create tensor of ones with same shape
x_ones = torch.ones_like(x_data)
# Output: tensor([[1, 1], [1, 1]])

# Create random tensor with same shape but different type
x_rand = torch.rand_like(x_data, dtype=torch.float)
# Output: tensor([[0.4815, 0.7297], [0.8659, 0.5418]])
```

The `rand_like()` method fills the tensor with random numbers from a uniform distribution over [0, 1).

**Creating tensors with specific shapes**:

```python
shape = (2, 5)
rand_tensor = torch.rand(shape)    # Random values in [0, 1)
ones_tensor = torch.ones(shape)    # All ones
zeros_tensor = torch.zeros(shape)  # All zeros
```

**Summary of creation methods**:
- `torch.tensor(data)` - from data
- `torch.from_numpy(array)` - from NumPy
- `ones_like()`, `rand_like()` - with same shape
- `torch.rand()`, `torch.ones()`, `torch.zeros()` - with specific shape

---

## 1.3 Tensor Attributes

Every tensor has three key attributes: shape, data type, and device location.

```python
tensor = torch.rand(3, 4)  # Create a 3×4 tensor

print(f"Shape: {tensor.shape}")      # torch.Size([3, 4])
print(f"Datatype: {tensor.dtype}")   # torch.float32
print(f"Device: {tensor.device}")    # cpu
```

**Shape**: `tensor.shape` returns dimensions. `torch.Size([3, 4])` means 3 rows and 4 columns.

**Data Type**: Common PyTorch types include `torch.float32` (default floating-point), `torch.int64` (integers), and `torch.bool` (boolean).

**Device**: Indicates storage location - `cpu` for CPU memory or `cuda:0` for GPU.

**Moving tensors to GPU**:

```python
if torch.cuda.is_available():
    tensor = tensor.to('cuda')
```

Understanding these attributes is crucial for memory management, ensuring compatible operations, and optimizing computation with GPU acceleration.

---

---

## 1.4 Tensor Indexing and Slicing

Tensors support various operations including transposition, indexing, slicing, mathematical operations, linear algebra, and random sampling. These operations can run on GPU for significantly faster computation.

**GPU acceleration**: GPUs have lower computing power per core but many more cores than CPUs, making them excellent for parallel computation. In deep learning, GPU computation is much faster than CPU. CUDA (Nvidia's parallel computing framework) and cuDNN (for deep convolutional networks) enable this acceleration.

**Moving tensors to GPU**:
```python
if torch.cuda.is_available():
    tensor = tensor.to('cuda')
    print(f"Device tensor is stored on: {tensor.device}")
```

**Indexing and slicing**:
```python
tensor = torch.ones(4, 4)  # Create 4×4 tensor of ones
print(tensor)
# Output: 4×4 matrix of all ones

tensor[:, 1] = 0  # Set all rows, second column to 0
# Syntax: [first_dimension, second_dimension]
# : means "from start to end with step 1"
print(tensor)
# Output: 
# tensor([[1., 0., 1., 1.],
#         [1., 0., 1., 1.],
#         [1., 0., 1., 1.],
#         [1., 0., 1., 1.]])
```

---

## 1.5 Tensor Concatenation

Use `torch.cat()` to concatenate multiple tensors along a specified dimension.
```python
tensor = torch.ones(4, 4)
tensor[:, 1] = 0

# Concatenate along dimension 1 (columns, horizontally)
t1 = torch.cat([tensor, tensor, tensor], dim=1)
# Result: 4×12 tensor (three 4×4 tensors side by side)
```

**Understanding dimensions**: For 2D arrays, `dim=0` refers to rows (vertical concatenation), `dim=1` refers to columns (horizontal concatenation).

**More examples**:
```python
A = torch.ones(2, 3)      # 2×3 tensor
B = 2 * torch.ones(4, 3)  # 4×3 tensor

# Concatenate along rows (vertically)
C = torch.cat([A, B], dim=0)  # Result: 6×3 tensor

D = 2 * torch.ones(2, 4)  # 2×4 tensor

# Concatenate along columns (horizontally)
E = torch.cat([A, D], dim=1)  # Result: 2×7 tensor
```

---

## 1.6 Tensor Arithmetic Operations

Tensors support element-wise arithmetic operations with automatic broadcasting.
```python
x = torch.tensor([[[1, 2, 3],
                   [4, 5, 6]],
                  [[7, 8, 9],
                   [10, 11, 12]]])  # 3D tensor

y = torch.tensor([1, 2, 3])  # 1D tensor

result = y - x
# Broadcasting applies: y is expanded to match x's shape
# Each row of x is subtracted from y element-wise
```

---

## 1.7 Broadcasting Mechanism

**Broadcasting** allows PyTorch operations to work on tensors of different shapes without explicitly copying data, enabling efficient computation.

**Broadcasting conditions**:

1. **Both tensors must have at least one element**
```python
x = torch.empty(0,)       # Cannot broadcast - empty
y = torch.empty(2, 2)

x = torch.empty(1,)       # Can broadcast - has one element
y = torch.empty(2, 2)
```

2. **Dimensions must be compatible when compared right-to-left**

Dimensions are compatible if:
- **a)** They are equal in size
- **b)** One tensor is missing that dimension
- **c)** One tensor has size 1 in that dimension

**Example**:
```python
x = torch.empty(5, 3, 4, 1)
y = torch.empty(   3, 1, 1)
```

Checking from right to left:
- 4th dimension: both size 1 ✓ (condition a)
- 3rd dimension: 4 vs 1 ✓ (condition c)
- 2nd dimension: both size 3 ✓ (condition a)
- 1st dimension: 5 vs missing ✓ (condition b)

**Broadcasting process**:

Step 1 - Align dimensions by adding size-1 dimensions:
```python
# Before alignment:
x = torch.empty(5, 3, 4, 1)
y = torch.empty(   3, 1, 1)

# After alignment:
x = torch.empty(5, 3, 4, 1)
y = torch.empty(1, 3, 1, 1)
```

Step 2 - Expand size-1 dimensions to match:
```python
# Before expansion:
x = torch.empty(5, 3, 4, 1)
y = torch.empty(1, 3, 1, 1)

# After expansion (ready for operation):
x = torch.empty(5, 3, 4, 1)
y = torch.empty(5, 3, 4, 1)
```

**Key rule**: If two dimensions are unequal and neither is 1, broadcasting is not possible.

---

# Chapter 2: Derivatives, Differentials, and Gradients

## 2.1 Derivatives of Composite Functions

**Chain Rule**: When differentiating composite functions, work from the outside in, taking derivatives layer by layer. Multiply the derivative of the outermost function by the derivative of the inner function.

**Product Rule (Leibniz Formula)**: For products of two functions like $x^{\ln x}$:

$$(u \cdot v)' = u' \cdot v + u \cdot v'$$

This is the cross-derivative rule: differentiate each function while keeping the other constant, then sum.

Example: $(x \cdot \ln x)' = 1 \cdot \ln x + x \cdot \frac{1}{x} = \ln x + 1$

**Quotient Rule**: For quotients:

$$\left(\frac{v}{u}\right)' = \frac{v' \cdot u - v \cdot u'}{u^2}$$

**Example 1 - Exponential with quotient**: Find the derivative of $y = 2^{x/\ln x}$

Solution:
1. Apply chain rule: $y' = 2^{x/\ln x} \cdot \ln 2 \cdot \left(\frac{x}{\ln x}\right)'$

2. Apply quotient rule: $\left(\frac{x}{\ln x}\right)' = \frac{\ln x - 1}{(\ln x)^2}$

3. Final result: $y' = 2^{x/\ln x} \cdot \ln 2 \cdot \frac{\ln x - 1}{(\ln x)^2}$

**Example 2 - Logarithmic differentiation**: Find the derivative of $y = (1+2x)^x$

Solution:
1. Use logarithmic identity: $y = e^{\ln((1+2x)^x)} = e^{x \cdot \ln(1+2x)}$

2. Apply chain and product rules: $y' = e^{x \cdot \ln(1+2x)} \cdot [1 \cdot \ln(1+2x) + x \cdot (\ln(1+2x))']$

3. Find inner derivative: $(\ln(1+2x))' = \frac{2}{1+2x}$

4. Final result: $y' = (1+2x)^x \cdot \left[\ln(1+2x) + \frac{2x}{1+2x}\right]$

**Key takeaway**: Work layer by layer - identify the outermost function, apply the appropriate rule (chain, product, or quotient), continue differentiating inner functions, and combine all derivatives through multiplication.
