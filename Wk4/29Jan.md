---
title: Digital Signal Analysis (CS7.303)
subtitle: |
          | Spring 2022, IIIT Hyderabad
          | 29 Jan, Saturday (Lecture 7)
author: Taught by Prof. Anil Kumar Vuppala
---

# Circular Convolution
Circular convolution is an operation that generalises ordinary (linear) convolution to periodic functions. It is used in DFT as the input and output of that transform are required to be periodic with period $N$.  

We know that in the ordinary Fourier transform, the linear convolution of two functions is converted to their product. In DFT, the corresponding relation is
$$x_1(n) \otimes x_2(n) \to X_1(k) \cdot X_2(k).$$

If we want to take the circular convolution of two sequences of lengths $L_1, L_2$, then the result will have length $\max(L_1, L_2)$. It is computed as
$$x_1(n) \otimes x_2(n) = \sum_{m=0}^{N-1} x_1(m) x_2(n-m),$$
where $x_1$ and $x_2$ are periodic with period $N$. A matrix formulation is
$$\begin{bmatrix}
x_1(0) & x_1(N-1) & \cdots & x_1(1) \\
x_1(1) & x_1(0) & \cdots & x_1(2) \\
\vdots & \vdots & \ddots & \vdots \\
x_1(N-1) & x_1(N-2) & \cdots & x_1(0) \end{bmatrix}
\begin{bmatrix} x_2(0) \\ x_2(1) \\ \vdots \\ x_2(N-1) \end{bmatrix}$$

We can also calculate the linear convolution using the circular convolution by taking the period $N$ to be $L_1 + L_2 - 1$, the length of the linear convolution.

# Fast Fourier Transform
## Motivation
We have seen that the $N$-point DFT of $x(n)$ can be calculated by multiplying the $W$ matrix
$$\begin{bmatrix}
1 & 1 & \cdots & 1 \\
1 & w_N & \cdots & w_N^{N-1} \\
\vdots & \vdots & \ddots & \vdots \\
1 & w_N^{N-1} & \cdots & w_N^{(N-1)^2} \end{bmatrix}$$
by the column vector $x$. This multiplication takes a huge number of operations, typically $O(N^2)$ (even assuming that the powers of $w_N$ are precomputed).  

FFT is an algorithm to solve this problem by applying the principle of divide and conquer. It uses two $\frac{N}2$-point DFTs to compute the $N$-point DFT. The number of operations involved using the FFT algorithm is $O(N\log N)$.
