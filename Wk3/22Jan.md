---
title: Digital Signal Analysis (CS7.303)
subtitle: |
          | Spring 2022, IIIT Hyderabad
          | 22 Jan, Saturday (Lecture 5)
author: Taught by Prof. Anil Kumar Vuppala
---

# Systems (contd.)
## LTI Systems
LTI systems are those which are both linear and time-invariant. For example, consider the system
$$y(n) = ay(n-1) + x(n).$$

An important characteristic of an LTI system is its *impulse response*, *i.e.*, its output when the input is the impulse $\delta(n)$. It is denoted $h(n)$.  

LTI systems have the property that $y(n) = x(n) \* h(n)$, *i.e.*, the output is the convolution of the input with the impulse response. We will prove this for discrete systems.  

It can be shown that
$$x(n) = \sum_{k=-\infty}^\infty x(k)\delta(n-k),$$
as $\delta(n-k)$ becomes 1 only for $k=n$, which makes the value of the sum $x(n)$.  

Now, we apply the system on both sides.  
As it is linear, we can consider each term separately.  
In each term, we have a constant coefficient $x(k)$ and a time-shifted impulse $\delta(n-k)$.  
By time-invariance, however, this is simply $h(n-k)$.  

Putting all this together, we get
$$y(n) = \sum_{k=-\infty}^\infty x(k)h(n-k),$$
which is the same as
$$y(n) = x(n) \* h(n).$$

Note that when taking the convolution, we let $n$ be $l_1 + l_2 -1$, where $l_1$ is the number of nonzero values of $x(n)$, and $l_2$ the number of nonzero values of $h(n)$. This is called a *linear convolution*.  

The impulse response of an LTI system also helps us determine if it is causal or not. An LTI system is causal iff
$$h(n) = 0, \forall n < 0.$$

Similarly, an LTI system is stable iff
$$\sum_{k=-\infty}^\infty |h(k)|$$
is finite.

# Sampling and Quantisation
Sampling and quantisation are two processes carried out on signals. Analog signals are converted to discrete ones by sampling, and discrete ones to digital ones by quantisation.

## Sampling
For information to not be lost in the process of sampling, the frequency of sampling $f_S$ has a minimum bound given by the Nyquist criterion:
$$f_S \geq 2f_m,$$
where $f_m$ is the frequency of the analog input signal.

## Quantisation
Quantisation involves discretising the output of the signal, given the number of bits $N$ and the range $[l, u]$. The expression for the step size given these parameters is
$$\frac{(u-l)}{2^N}.$$

The maximum quantisation error is given by half the step size.
