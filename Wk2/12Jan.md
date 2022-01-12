---
title: Digital Signal Analysis (CS7.303)
subtitle: |
          | Spring 2022, IIIT Hyderabad
          | 12 Jan, Wednesday (Lecture 3)
author: Taught by Prof. Anil Kumar Vuppala
---

# Fourier Series and Transform
## Fourier Transform
### Properties of FT (contd.)
Convolution is a mathematical operator on two functions, that produces a third function which expresses how one affects the shape of the other. It is defined as
$$(f * g)(t) = \int_{-\infty}^\infty f(\tau)g(t - \tau)d\tau = \int_{-\infty}^\infty f(t-\tau)g(\tau)d\tau.$$

The convolution property of the Fourier transform states that if
$$\begin{split}
x(t) &\to X(\omega) \\
h(t) &\to H(\omega), \end{split}$$
then
$$\begin{split}
x(t) * h(t) &\to X(\omega) \cdot H(\omega) \\
x(t) \cdot h(t) &\to X(\omega) * H(\omega) \end{split}$$

This can be easily proved:
$$\begin{split}
F \left[ f_1(t) * f_2(t) \right] &= \int_{-\infty}^\infty \left[ f_1(t) * f_2(t) \right] e^{-j\omega t}dt \\
&= \int_{-\infty}^\infty \int_{-\infty}^\infty f_1(\tau)f_2(t - \tau)e^{-j\omega t} d\tau dt \\
&= \int_{-\infty}^\infty f_1(\tau) \left[ \int_{-\infty}^\infty f_2(t-\tau)e^{-j\omega t} dt \right] d\tau \\
&= \int_{-\infty}^\infty f_1(\tau) F_2(\omega) e^{-j\omega\tau}d\tau \\
&= F_1(\omega) F_2(\omega). \end{split}$$

### Discrete-Time Fourier Transform
As the Fourier transform takes as input and gives as output continuous real-valued functions, it is not possible for computers to compute it exactly. The discrete-time fourier transform overcomes this difficulty by simply taking the value of the input $x(t)$ at discrete values $n$:
$$X\left(e^{j\omega}\right) = \sum_{n=-\infty}^\infty x(n) e^{-j\omega n}$$

$x(n)$ is defined as $x(t) \cdot \delta(t)$, where $\delta(t)$ is the *impulse train* (its value is zero everywhere except at discrete inputs separated by $T_s$, where it is infinite). Writing the input as $X\left(e^{j\omega}\right)$ makes it periodic (introducing discretisation in one domain introduces periodicity in the other).  

**More Details.**  
Say we have a continuous function $m(t)$ and an impulse train $\delta(t)$, with an infinite value at inputs separated by $T_s$. Note that the integral across each spike is 1.  

We can find the Fourier series of $\delta(t)$:
$$\delta(t) = \frac1{T_s} \left[ 1 + \sum_{n=1}^\infty 2\cos(n \omega_0 t) \right].$$

Now, we multiply $m(t)$ with $\delta(t)$ to sample it:
$$g(t) = \frac1{T_s} \left[ m(t) + 2\cos (\omega_0 t) m(t) + 2 \cos (2\omega_0 t) m(t) + \cdots \right].$$
We can express this in complex form
$$g(t) = \frac1{T_s} \left[ m(t) + e^{-j\omega_0 t} m(t) + e^{j \omega_0 t} m(t) + e^{-2j\omega_0 t}m(t) + e^{2j\omega_0 t}m(t) + \cdots \right],$$

which makes it easy to calculate the Fourier transform:
$$G(\omega) = \frac1{T_s} \left[ M(\omega) + M(\omega + \omega_0) + M(\omega - \omega_0) + M(\omega + 2\omega_0) + M(\omega - 2\omega_0) + \cdots \right]$$

If $M(\omega)$ has some cutoff frequency $f_m$ (*i.e.* for values $> f_m$ or $< -f_m$, it is zero), then $G(\omega)$ will have a number of possibly overlapping regions. This intereference is called aliasing.  
The Nyquist Sampling Theorem tells us the minimum sampling rate $f_s = \frac1{T_s}$ to avoid aliasing:
$$f_s \geq 2f_m$$

The discrete-time Fourier transform can be inverted:
$$x(n) = \frac1{2\pi} \int_T X \left(e^{j\omega}\right)e^{j\omega n}d\omega.$$

### Discrete Fourier Transform
The DTFT, however, outputs a continuous real-valued function, like the FT. The discrete Fourier transform samples the output function as well, at discrete values $k$, in order to avoid this.
$$X(k) = \sum_{n=0}^{N-1} x(n) e^{-\frac{2\pi j n k}{N}}, k \in \{0, \dots, N-1\}.$$

This is called the $N$-point DFT. Here, we require $x(t)$ to be periodic with period $N$; thus we take $x_p(n)$, a periodic version of $x(t)$.
