---
title: Digital Signal Analysis (CS7.303)
subtitle: |
          | Spring 2022, IIIT Hyderabad
          | 24 Jan, Monday (Lecture 6)
author: Taught by Prof. Anil Kumar Vuppala
---

# Discrete Fourier Transform
We know that the Fourier transform of a continuous fuction $x(t)$ is denoted as $X(\omega)$ and is also continuous. When we discretise the input by sampling, we obtain $X(e^{j \omega})$, the discrete-time Fourier transform of $x(n)$, which is the periodic version of $X(\omega)$.  
However, to solve the problem caused by the output function being continuous, we define the discrete Fourier transform, which takes $x(n)$ to $X(k)$, a sampled version of $X(e^{j\omega})$.  
An important parameter in DFT is $N$, which determines the period of $X(k)$. We calculate the $N$-point DFT, which samples $X(e^{j\omega})$ at $N$ values. Usually, $N$ is taken to be a power of 2.  
Note that $N$ must be greater than or equal to the number of values at which $x(n)$ is defined.  

Clearly, greater values of $N$ are better for us, as they increase accuracy. However, if $x(n)$ is defined for fewer than $N$ values, we carry out *zero-padding* – we give $x(n)$ a value of 0 at the remaining points, so as to ensure that it has $N$ values, and we can then compute the $N$-point DFT.  

It is common to substitute
$$w_N = e^{\frac{-2\pi j}{N}},$$
often called the *twiddle factor*. This allows us to write
$$X(k) = \sum_{n=0}^{N-1} x(n)w_N^{kn}.$$

We can write this expression in matrix notation:
$$\begin{bmatrix} X(0) \\ X(1) \\ \vdots \\ X(N-1) \end{bmatrix} =
\begin{bmatrix} 1 & 1 & \cdots & 1 \\
1 & w_N & \cdots & w_N^{N-1} \\
\vdots & \vdots & \ddots & \vdots \\
1 & w_N^{N-1} & \cdots & w_N^{(N-1)^2} \end{bmatrix}
\begin{bmatrix} x(0) \\ x(1) \\ \vdots \\ x(N-1) \end{bmatrix}.$$

The parameter $N$ adds a caveat to the linearity property of DFT: the DFT of $ax_1(n) + bx_2(n)$ is $aX_1(k) + bX_2(k)$ iff each of the DFTs of $x_1(n)$ and $x_2(n)$ are w.r.t the same value of $N$.  

Assuming that $x(n)$ is periodic with period $N$ means that we have to carry out *circular shift* to find its values at other points. Linear shifting is *not* applicable in DFT.  
Another property that must be changed is convolution – in DFT we carry out only the *circular convolution* of functions.
