---
title: Digital Signal Analysis (CS7.303)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | 05 Jan, Wednesday (Lecture 1)
author: Taught by Prof. Anil Kumar Vuppala
---

# Introduction
A *signal* is a parameter that depends on another independent parameter, which usually carries some information. For example, voltage be considered as a function of time is a signal.  
Signals can be single- or multi-dimensional (decided by the number of independent parameters). For example, images are two-dimensional, depending on two spatial coordinates ($x$ and $y$, or $r$ and $\theta$).  

*Processing* or *analysis* is carried out on signals in order to extract the information carried by them, or in order to manipulate them in some way (for example, to amplify sound signals).  

A number of useful signals, like speech and images, are analog (continuous, in this case w.r.t time). However, we process them by digital devices. Thus analog signals have to be converted to digital ones in order for processing.  

In the case of a non-analog (sampled) signal, when the dependent parameter is taken from a continuous space (like the real numbers), the signal is called *discrete*; if the dependent parameter is mapped to a discrete space (like binary strings), the signal is called *digital*. Only digital signals can be processed by computers; discrete signals cannot.

# Fourier Series and Transforms
The Fourier transform, based on the Fourier series, is a method for converting analog to discrete signals.  

## Fourier Series
The Fourier series is based on the fact that any **periodic signal** can be represented as a sum of sines and cosines with the appropriate coefficients (*i.e.* as a linear combination of sines and cosines).
$$f(t) = a_0 + \sum_{n=1}^\infty a_n \cos \left(2 \pi n \frac{t}{T}\right) + \sum_{n=1}^\infty b_n \sin \left(2\pi n \frac{t}{T} \right),$$
where $T$ is the period of $f$. We sometimes write $\omega_0$ for $\frac{2\pi}{T}$.  

The coefficients can be calculated as
$$\begin{split}
a_n &= \frac{2}{T} \int_0^T f(t) \cos \left(2\pi n \frac{t}{T}\right) dt \\
b_n &= \frac{2}{T} \int_0^T f(t) \sin \left(2\pi n \frac{t}{T} \right) dt.\end{split}$$
These can be derived by multiplying by sine and cosine, and integrating, both sides of the first identity.
