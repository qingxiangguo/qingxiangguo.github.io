---
title: 'Chapter 2: Derivatives, Differentials, and Gradients'
date: '2025-01-17'
summary: 'Understanding derivatives of composite functions, product rule, quotient rule, and L'Hôpital's rule'
tags:
  - Deep Learning
  - Calculus
  - Derivatives
---

## 2.1 Derivatives of Composite Functions

### Chain Rule

When finding the derivative of a composite function, we work **from the outside in**, taking derivatives layer by layer. The outermost function is differentiated first, multiplied by the derivative of the inner function, and so on.

### Product Rule (Leibniz Formula)

When dealing with high-order functions like $x^{\ln x}$ that involve products of two functions, we use the **Leibniz formula** (also called the product rule):

$$(u \cdot v)' = u' \cdot v + u \cdot v'$$

This is the **cross-derivative rule**: differentiate each function while keeping the other constant, then sum the results.

**Example:**

$$(x \cdot \ln x)' = x' \cdot \ln x + x \cdot (\ln x)' = 1 \cdot \ln x + x \cdot \frac{1}{x} = \ln x + 1$$

### Quotient Rule

For the derivative of a quotient:

$$\left(\frac{v}{u}\right)' = \frac{v' \cdot u - v \cdot u'}{u^2}$$

### Worked Example 1: Exponential with Quotient

Find the derivative of $y = 2^{x/\ln x}$

**Solution:**

1. Apply the chain rule. Since the derivative of $a^x$ is $a^x \ln a$:
   $$y' = 2^{x/\ln x} \cdot \ln 2 \cdot \left(\frac{x}{\ln x}\right)'$$

2. Apply the quotient rule to $\left(\frac{x}{\ln x}\right)'$:
   $$\left(\frac{x}{\ln x}\right)' = \frac{x' \cdot \ln x - x \cdot (\ln x)'}{(\ln x)^2} = \frac{1 \cdot \ln x - x \cdot \frac{1}{x}}{(\ln x)^2} = \frac{\ln x - 1}{(\ln x)^2}$$

3. Final result:
   $$y' = 2^{x/\ln x} \cdot \ln 2 \cdot \frac{\ln x - 1}{(\ln x)^2}$$

### Worked Example 2: L'Hôpital's Rule

Find the derivative of $y = (1+2x)^x$

**Solution:**

1. Use the **logarithmic identity** (also known as L'Hôpital's rule approach):
   $$y = e^{\ln((1+2x)^x)}$$

2. Simplify using logarithm properties:
   $$y = e^{x \cdot \ln(1+2x)}$$

3. Apply the chain rule and product rule:
   $$y' = e^{x \cdot \ln(1+2x)} \cdot (x \cdot \ln(1+2x))'$$

4. Apply the product rule to $(x \cdot \ln(1+2x))'$:
   $$y' = e^{x \cdot \ln(1+2x)} \cdot [1 \cdot \ln(1+2x) + x \cdot (\ln(1+2x))']$$

5. Find $(\ln(1+2x))'$ using the chain rule:
   $$(\ln(1+2x))' = \frac{1}{1+2x} \cdot 2 = \frac{2}{1+2x}$$

6. Substitute back:
   $$y' = (1+2x)^x \cdot \left[\ln(1+2x) + \frac{2x}{1+2x}\right]$$

### Key Takeaway

The process is to **work layer by layer**:
1. Identify the outermost function
2. Apply the appropriate rule (chain, product, or quotient)
3. Continue differentiating inner functions
4. Combine all derivatives using multiplication
