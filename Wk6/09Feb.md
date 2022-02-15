---
title: Digital Signal Analysis (CS7.303)
subtitle: |
          | Spring 2022, IIIT Hyderabad
          | 09 Feb, Wednesday (Lectures 9 & 10)
author: Taught by Prof. Anil Kumar Vuppala
---

# Z-Transform
We have seen that the discrete-time Fourier transform is given by
$$X(e^{j\omega}) = \sum_{n=-\infty}^\infty x(n)e^{-j\omega n}.$$

However, this expression may not always converge. The Z-transform, therefore, takes care of this by adding another parameter:
$$X(z) = \sum_{n=-\infty}^\infty x(n) z^{-n},$$
where $z = re^{j \omega}$. By choosing $z$ appropriately (within the region of convergence or RoC), we can ensure that $X(z)$ converges.

## Examples
We will consider five examples of the Z-transform.  

First, let $x(n) = \delta(n)$. Then we have
$$X(z) = \sum_{n=-\infty}^\infty \delta(n) z^{-n} = 1.$$
The RoC is the entire $z$-plane in this case.  

Next, consider $x(n) = \delta(n-k)$. Then,
$$X(z) = \sum_{n=-\infty}^\infty \delta(n-k) z^{-n} = z^{-k}.$$
Here, the RoC is $\mathbb{C}$ if $k=0$, $\mathbb{C} - \{0\}$ if $k>0$, and $\mathbb{C} - \{\infty\}$ if $k<0$.  

Third, we have $x(n) = \{4,3,0,1\}$, with $x(0) = 3$. This gives us
$$X(z) = 4z + 3 + \frac1{z^2},$$
and so the RoC is $\mathbb{C} - \{0,\infty\}$.  

Fourth, let $x(n) = p^n u(n)$. Then we get
$$\begin{split}
X(z) &= \sum_{n=-\infty}^\infty p^n u(n) z^{-n} \\
&= \sum_{n=0}^\infty \left(\frac{p}{z}\right)^n \\
&= \frac{z}{z-p}. \end{split}$$
For the RoC,
$$\left|\frac{p}{z}\right| < 1,$$
which means that
$$|z| = r > |p|.$$

Lastly, we take $x(n) = -p^n u(-n-1)$. Then,
$$\begin{split}
X(k) &= \sum_{n=-\infty}^{-1} -\left(\frac{p}{z}\right)^n \\
&= -\sum_{k=1}^\infty \left(\frac{p}{z}\right)^k \\
&= -\frac{p}{z} \cdot \frac{1}{1-\frac{p}{z}} \\
&= \frac{z}{z-p}. \end{split}$$
The RoC here is
$$|z| = r < |p|.$$
Note that the expression for $X(z)$ is the same as in example 4, but the RoC is different. Example 4 is a right-side signal, while example 5 is a left-side signal.

If $x(n)$ is expressed as $x_1(n) + x_2(n) + \cdots$, then its RoC is given by $R_1 \cap R_2 \cap \cdots$. Also, the Z-transform is linear.

## Properties
By the time-shifting property of the Z-transform, if $x(n)$ transforms to $X(z)$ with RoC $R$, then $x(n-k)$ transforms to $z^{-k}X(z)$.  
The RoC for this is $R - \{0\}$ if $k > 0$, and $R - \{\infty\}$ if $k < 0$.  

Scaling in the $z$-domain is related to exponential rise in the time domain; thus $a^nx(n)$ transforms to $X\left(\frac{z}{a}\right)$.  
The RoC changes from $z \in R$ to $\frac{z}{a} \in R$.  

Similarly, the time inversion property states that $x(-n)$ transforms to $X\left(\frac1z\right)$.  
The RoC, here too changes to $\frac1z \in R$.  

Furthermore, $nx(n)$ transforms to $-z\frac{d}{dz}X(z)$.  

Let $x_1(n)$ and $x_2(n)$ transform to $X_1(z)$ and $X_2(z)$, with RoCs $R_1$ and $R_2$ respectively. Then the convolution $x_1(n) * x_2(n)$ transforms to $X_1(z) \cdot X_2(n)$.  
This property can be used to solve LTI systems. We know that $y(n) = x(n) * h(n)$; thus we can find $Y(z) = X(z) * H(z)$ and find the inverse Z-transform to obtain $y(n)$.  

Furthermore, the initial value theorem states that
$$x(0) = \lim_{z\to\infty}X(z),$$
and the final value theorem states that
$$\lim_{n\to\infty} x(n) = \lim_{z\to 1} (z-1)X(z).$$

## Inverse Z-Transform
To take the inverse Z-transform, we can employ several methods, like:

* contour integration
* table lookup
* using properties
* series expansion (by long division or other methods)
* partial fractions

Note that if the RoC is not given, we assume $X(z)$ to be a right-side signal, *i.e.*, take the rightmost possible RoC.  

The RoC may change the signal we obtain. For example, consider the signal
$$X(z) = \frac{a}{1-\frac{b}{z}}.$$
If the RoC is given to be $|z| > |b|$, then the inverse is
$$x(n) = ab^nu(n),$$
which is called the right-side signal. However, if the RoC is $|z| < |b|$, then the inverse is
$$x(n) = -ab^nu(-n-1),$$
*i.e.*, the left-side signal.  

## Application
Consider a digital system given by
$$y(n) + 0.1y(n-1) - 0.2y(n-2) = x(n) + x(n-1),$$
and we need to find $h(n)$. We can do this by converting to the $z$-domain:
$$Y(z) + 0.1z^{-1}Y(z) - 0.2z^{-2}Y(z) = X(z) + z^{-1}X(z).$$

Now we know that $H(z) = \frac{Y(z)}{X(z)}$, which gives us
$$H(z) = \frac{1+z^{-1}}{1+0.1z^{-1}-0.2z^{-2}}.$$
We can then calculate the IZT of $H(z)$ to find $h(n)$, which will come out to be
$$h(n) = 1.556(0.4)^nu(n) - 0.556(-0.5)^nu(n).$$
