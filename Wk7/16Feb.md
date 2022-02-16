---
title: Digital Signal Analysis (CS7.303)
subtitle: |
          | Spring 2022, IIIT Hyderabad
          | 16 Feb, Wednesday (Lecture 11)
author: Taught by Prof. Anil Kumar Vuppala
---

# Z-Transform (contd.)
## LTI Systems
A general LTI system can be expressed as
$$y(n) = -\sum_{k=1}^N a_k y(n-k) + \sum_{k=0}^M b_k x(n-k).$$
We can apply the Z-transform on both sides to get
$$Y(z) = -\sum_{k=1}^N a_k z^{-k} Y(z) + \sum_{k=0}^M b_k z^{-k}X(z),$$
which means that
$$H(z) = \frac{Y(z)}{X(z)} = \frac{\sum_{k=0}^M b_k z^{-k}}{1+\sum_{k=1}^N a_k z^{-k}}.$$

The values at which this expression becomes zero (the roots of the numerator) are called its *zeros*, while the values at which it becomes infinity (the roots of the denominator) are called its *poles*.  

A system for which $a_i = 0$ for all $i$ is called an all-zero system. Such a system is always stable. It forms an FIR system.  

If $b_i = 0$ for all $i$, then the system is called an all-pole system. It then becomes an IIR system. It is not necessarily stable.  

## Causal and Stable Systems
We have seen that for an LTI system to be stable, $h(n) = 0$ for all $n < 0$. This means that $H(z)$ must be a right-side signal.  

We also know that for a stable LTI system,
$$\sum_{n=-\infty}^\infty |h(n)| < \infty.$$
By the definition of $H(z)$, we can see that $H(1) < \infty$. Thus the RoC should contain the unit signal.  
We know that FIR systems are always stable. An IIR system is stable if all its poles lie inside the unit circle.

## Natural and Forced Responses
When we solve an LTI system using the Z-transform, we usually obtain two terms – one due to $X(z)$ and one due to $H(z)$.  
The former is called the *natural* or *transient* response (it decays) and the latter the *forced* or *steady-state* response.

# Filter Design
A filter is a system that suppresses unwanted frequencies in its input.  

There are four kinds of filters: low-pass, high-pass, band-pass and band-rejection. Low-pass filters stop all frequencies above a certain bound; high-pass filters stop all those below it. A band-pass filter allows only a limited range of frequencies (bounded above and below), and a band-rejection filter allows all frequencies *not* in a limited range.  

However, it is not possible to design an ideal filter which stops exactly those frequencies above a certain $f$. Instead, there is usually a *transition band* centred around $f$, and a *stop band* (in which the amplitudes are very small, but not necessarily zero) after this.  

The design of filters rests on identifying the values of $a_i$ and $b_i$ and realising the LTI system (using delays, multipliers and adders).  

It is important when designing a filter to ensure that the poles are not too close to the boundary of the unit circle. This is because the quantisation error might perturb the poles so that they lie outside, causing the system to become unstable.