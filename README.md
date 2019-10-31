# ME 701 - Homework 7

Solve the following problems.  Include unit tests!

## Problem 1 - File Processing and String Manipulation


Use only `str` functions to read `pwr.log` and produce two arrays, one
for `kinf` and one for `burnup`.  Note, these correspond to the second
and third full columns, i.e., `burnup = [0, 0.1, 0.5, ...]` and
`kinf = [1.27354, 1.23449, ...]` in the following:

```
                                             ****** *******
   NO VOID    TFU    TMO    TCO    BOR ROD   BURNUP   K-INF   K-INF     M2     PIN   U-235 FISS PU  TOT PU
                                             MWD/KG             TWO-GROUP     PEAK    WT %    WT %    WT %
    1  0.0  900.0  565.0  580.0  900.0        0.000 1.27354 1.27149  62.18   1.059   4.000   0.000   0.000  
    2                                         0.100 1.23449 1.23311  61.64   1.060   3.988   0.002   0.002  
    3                                         0.500 1.22571 1.22445  61.51   1.060   3.941   0.022   0.022  
    4                                         1.000 1.21976 1.21858  61.41   1.060   3.882   0.049   0.050  
```


## Problem 2 - Regex

Write a Python function named `five_chars(s)` to find all five character long words in a string `s`.  You must use `re`.




## Problem 3 - Fun Plots

We are interested in examining how a time dependent problem changes with a parameter. We shall
investigate the time dependent heat transfer equation in 1-D, i.e.,

$$
  \frac{\partial T}{\partial t} = \alpha \frac{\partial^2 T}{\partial x^2} \, ,
$$

with $T(0, t) = 1$  and T(1, t) = 0. We know that after an infinite amount of time, the solution is linear in x, but how do the
solutions is linear in $x$, but how do the solutions vary for a fixed time?

Here's a short program for estimating the temperature over time:

```python
import numpy as np
import matplotlib.pyplot as plt
alpha = 1
def getTemp(alpha, L=1, tMax=0.1):
    dt = 0.00005
    dx = 0.01
    Nx = int(L / dx)
    dx = L / Nx
    Nt = int(tMax / dt)
    dt = tMax / Nt
    dx = L / Nx
    dt = tMax / Nt
    assert dt * alpha / dx ** 2 <= 0.5, 'Parameters are not numerically stable'
    temp = np.zeros(Nx)
    temp[0] = 1
    for i in range(Nt):
        temp[1:-1] += dt * alpha / dx ** 2 * (temp[0:-2] - 2 * temp[1:-1] +
            temp[2:])
    return temp, np.linspace(0, L, Nx)

T, x = getTemp(alpha)
plt.plot(x, T)
```


Your task is to produce an animation showing how the solution
changes with increasing $\alpha$.  Explore the parameter range $\alpha \in [0, 1]$.


