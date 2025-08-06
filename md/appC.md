# 

## Method of Least Squares

The following section is derived from Sedgewick \[1983\] and Kreyszig
\[1979\].

Suppose we have three points $x_1$, $x_2$, and $x_3$ and corresponding
values $y_1$, $y_2$, and $y_3$ which are to be fitted to a function of
the form $f(x) = c_1 f_1(x)\ + \ c_2 f_2(x)$. The goal is to find a
choice of coefficients $c_1$ and $c_2$ which minimizes the least square
error.

in $E \  = \ (c_1 f_1(x_1) \  + \  c_2 f_2(x_1) \ - \ y_1)^2 \ +$

in $(c_1 f_1(x_2) \  + \  c_2 f_2(x_2) \ - \ y_2)^2 \ +$

in $(c_1 f_1(x_3) \  + \  c_2 f_2(x_3) \ - \ y_3)^2 \ +$

To find the choices of $c_1$ and $c_2$ which minimizes this error, we
simply need to set the derivatives $dE \over dc_1$ and $dE
\over dc_2$ equal to zero.

For example, given the straight line $y = a + bx$ the sum of squares can
be defined as

$$E = \sum_{j = 1}^n (y_j - a - bx_j)^2$$

In order to find the minimum we need to take the partial derivative with
respect to both a and b.

$${\partial E \over \partial a} = - 2 \sum (y_j - a - bx_j) = 0$$

$${\partial E \over \partial b} = - 2 \sum x_j (y_j - a -
bx_j) = 0$$

Thus the normal equations are

$$an + b \sum x_j \ = \ \sum y_j$$

$$a \sum x_j + b \sum x_j^2 \ = \ \sum x_j y_j$$

Given the points

(-1.0,1.000),  (-0.1,1.099),  (0.2,0.808),  (1.0,1.000).

We calculate $n = 4$,

$\sum x_j = 0.1$,

$\sum x_j^2 = 2.05$,

$\sum y_j = 3.907$,

$\sum x_j y_j = 0.0517$

Hence the normal equations are

$4a + 0.10b = 3.9070$

$0.1a + 2.05b = 0.0517$

$a = 0.9773$ and $b = -0.0224$

and therefore the line is

$y = 0.9773 - 0.0224x$
