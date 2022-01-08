---
title: Digital Signal Analysis (CS7.303)
subtitle: |
          | Monsoon 2021, IIIT Hyderabad
          | 08 Jan, Saturday (Lecture 2)
author: Taught by Prof. Anil Kumar Vuppala
---

# Fourier Series and Transform
## Fourier Series (contd.)
The Fourier series, as we have seen, decomposes a periodic function into a linear combination of sines and cosines (the basis vectors in the vector space of functions).  

There are some conditions, called Dirichlet's conditions, under which the Fourier series of a function can be derived:

* $f(t)$ is a single-valued function in the interval $(t_1, t_2)$
* $f(t)$ has a finite number of discontinuities in the interval $(t_1, t_2)$
* $f(t)$ has a finite number of maxima and minima in the interval $(t_1, t_2)$
* $f(t)$ is absolutely integrable, *i.e.*,
$$\int_{t_1}^{t_2} |f(t)|dt < \infty.$$

When $f(t)$ satisfies all these conditions, it can be represented as
$$f(t) = a_0 + \sum_{n=1}^\infty a_n \cos (n \omega_0 t) + \sum_{n=1}^\infty b_n \sin(n \omega_0 t),$$
where
$$\begin{split}
a_0 = \frac1T \int_{t_0}^{t_0 + T} f(t) dt \\
a_n = \frac2T \int_{t_0}^{t_0 + T} f(t) \cos (n\omega_0t)dt \\
b_n = \frac2T \int_{t_0}^{t_0 + T} f(t) \sin (n\omega_0t)dt \end{split}$$

Each $n$ represents a different frequency and the constant $a_0$ represents the DC component of the signal.  

The complex Fourier series is also sometimes used:
$$f(t) = \sum_{n=-\infty}^\infty F_n e^{jn\omega_0 t},$$
where
$$F_n = \frac1T \int_{t_0}^{t_0 + T} f(t) e^{-jn\omega_0t}dt.$$

The equations expressing the function as the sum of sines are called *synthesis equations* and those giving the values of the coefficients are called *analysis equations*.

## Fourier Transform
The Fourier transform is simply the limit of the Fourier series as the time period goes to infinity:
$$F(\omega) = \lim_{T \to \infty} F(n)$$

Expressed fully,
$$F(\omega) = \int_{-\infty}^\infty f(t) e^{-j\omega t}dt.$$

Furthermore, it holds that
$$f(t) = \frac1{2\pi} \int_{-\infty}^\infty F(w) e^{j \omega t}dt.$$

The extra factor of $\frac1{2\pi}$ comes from Parseval's Theorem, which states that the energy in both domains must remain the same, and so the absolute integral of $F(\omega)$ and $f(t)$ must be equal.  

Consider, for example, the function which has the value $A$ for $-\frac{\tau}{2} \leq t \leq \frac{\tau}{2}$, and 0 elsewhere. We can calculate it as:
$$\begin{split}
F(w) &= \int_{-\infty}^\infty f(t)e^{-j\omega t}dt \\
&= \int_{-\frac{\tau}{2}}^{\frac{\tau}{2}} A e^{-j \omega t}dt \\
&= -\frac{A}{j \omega} e^{-j \omega t} \mid_{-\frac{\tau}{2}}^{\frac{\tau}{2}} \\
&= -\frac{A}{j \omega} 2\sin \left(-\frac{\omega\tau}2 \right) \\
&= \frac{A \tau}{2} 2\sin\left(-\frac{\omega\tau}{2} \right) \\
&= A \tau \text{sinc}\left(-\frac{\omega\tau}{2} \right). \end{split}$$

### Properties of FT
The Fourier transform is linear, *i.e.*,
$$a_1 f_t(t) + a_2 f_2 (t) \leftrightarrow a_1 F_1(\omega) + a_2 F_2 (\omega)$$

By the time-scaling property of Fourier transforms, if $f(t)$ transforms to $F(\omega)$, then $f(bt)$ transforms to $\frac1b F\left(\frac{\omega}b\right)$.  
By the time-shifting property, $f(t-b)$ transforms to $F(w) e^{-j\omega b}$.  

Furthermore, the $n^\text{th}$ differential of $f(t)$ transforms to $(j\omega)^nF(w)$. Conversely, $(-jt)^nf(t)$ transforms to the $n^\text{th}$ differential of $F(w)$.  

The Fourier transform, since it takes time period tending to infinity, is not only for periodic functions (unlike the Fourier series).  

The duality property of the Fourier transform states that, if $f(t)$ transforms to $F(\omega)$, then $F(t)$ has the transform $2\pi f(-\omega)$.
