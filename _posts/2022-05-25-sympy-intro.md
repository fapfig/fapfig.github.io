---
layout: post
title: Introduction to SymPy
categories: [Programming, Python, Sympy]
---

[![sympy](\assets\2022-05-25-sympy-intro\sympy.svg)](\assets\2022-05-25-sympy-intro\sympy.svg){:.glightbox}

[SymPy](https://www.sympy.org) is a Python library for symbolic mathematics. It aims to become a full-featured computer algebra system (CAS) while keeping the code as simple as possible in order to be comprehensible and easily extensible.

This post only shows some examples for solving equations, derivatives and integrals. For more complete tutorials please check the [SymPy Tutorial](https://docs.sympy.org/latest/tutorial/index.html#tutorial) website.

```python
from sympy import*

x, y, z = symbols("x, y, z", real=True)
init_printing(use_latex="mathjax")
```

## Solve

$$ x - 2 = 4$$

```python
solve(Eq(x-2,4),x)
```

$\displaystyle \left[ 6\right]$

$$ (x-3)(x-1) = 0 $$

If the argument of the solve function does not contain the word "Eq", thus SymPy will assume that the equation is equal to zero.

```python
solve((x-3)*(x-2),x)
```

$\displaystyle \left[ 2, \  3\right]$

$$ 5x^2 + 6x + 1 = 0 $$

```python
solve(5*x**2 + 6*x + 1, x)
```

$\displaystyle \left[ -1, \  - \frac{1}{5}\right]$

$$\begin{cases}  2x+4y=22\\−2x+2y=2\end{cases}$$

```python
solve([Eq(2*x+4*y, 22), Eq(-2*x+2*y, 2)], [x,y])
```

$\displaystyle \left\{ x : 3, \  y : 4\right\}$

```python
solve([2*x+4*y-22, -2*x+2*y-2], [x,y])
```

$\displaystyle \left\{ x : 3, \  y : 4\right\}$

## Derivatives

To take derivatives, use the `diff` function.

$$y=cos(x)$$

```python
diff(cos(x), x)
```

$\displaystyle - \sin{\left(x \right)}$

`diff` can take multiple derivatives at once. To take multiple derivatives, pass the variable as many times as you wish to differentiate, or pass a number after the variable. For example, both of the following find the third derivative of $x^4$.

```python
diff(x**4, x, x, x)
```

$\displaystyle 24 x$

```python
diff(x**4, x, 3)
```

$\displaystyle 24 x$

You can also take derivatives with respect to many variables at once. Just pass each derivative in order, using the same syntax as for single variable derivatives. For example, each of the following will compute

$$\frac{\partial^7}{\partial x \partial y^2 \partial z^4} e^{xyz}$$

```python
expr = exp(x*y*z)
diff(expr, x, y, y, z, z, z, z)
```

$\displaystyle x^{3} y^{2} \left(x^{3} y^{3} z^{3} + 14 x^{2} y^{2} z^{2} + 52 x y z + 48\right) e^{x y z}$

```python
diff(expr, x, y, 2, z, 4)
```

$\displaystyle x^{3} y^{2} \left(x^{3} y^{3} z^{3} + 14 x^{2} y^{2} z^{2} + 52 x y z + 48\right) e^{x y z}$

```python
diff(expr, x, y, y, z, 4)
```

$\displaystyle x^{3} y^{2} \left(x^{3} y^{3} z^{3} + 14 x^{2} y^{2} z^{2} + 52 x y z + 48\right) e^{x y z}$

To print the derivative, use the `Derivative` class.

```python
Derivative(expr, x, y, y, z, 4)
```

$\displaystyle \frac{\partial^{7}}{\partial z^{4}\partial y^{2}\partial x} e^{x y z}$

## Integrals

$\displaystyle \int (x-2)\ dx$

To compute this integral, use the `integrate` function.

```python
f = x-2

integrate(f)
```

$\displaystyle \frac{x^{2}}{2} - 2 x$

Use the command `Integral` to print an integral.

```python
Integral(f,x)
```

$\displaystyle \int \left(x - 2\right)\, dx$

```python
expr = Integral(log(x)**2, x)
expr
```

$\displaystyle x \log{\left(x \right)}^{2} - 2 x \log{\left(x \right)} + 2 x$

To later evaluate the integral, call `doit`.

```python
expr.doit()
```

$\displaystyle x \log{\left(x \right)}^{2} - 2 x \log{\left(x \right)} + 2 x$

To compute a definite integral, pass the argument (integration_variable, lower_limit, upper_limit). For example, to compute

$$\int_{0}^{oo}e^{-x} dx$$

```python
integrate(exp(-x), (x, 0, oo))
```

$\displaystyle 1$

As with indefinite integrals, you can pass multiple limit tuples to perform a multiple integral. For example, to compute

$$ \int\_{-oo}^{oo}e^{-x^2-y^2} dx dy $$

```python
integrate(exp(-x**2 - y**2), (x, -oo, oo), (y, -oo, oo))
```

$\displaystyle \pi$

## References

1. SymPy 1.10.1 documentation » [SymPy Tutorial](https://docs.sympy.org/latest/tutorial/index.html#tutorial)
