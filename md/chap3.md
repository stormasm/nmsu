# Local Linear Techniques

Although local linear techniques are not nearly as popular as back
propagation, they are actually a superior learning algorithm for two
main reasons. First and foremost, they are orders of magnitude faster in
execution time. Secondly, they are much easier to understand from a
mathematical point of view.

Local linear techniques are based on a simple information theoretic
concept stating that data points which are close to each other are more
significant than points which are further away. The main idea is given a
question; find an answer to the question by simply looking at the
neighbors nearest to the question. The fact that makes these methods
difficult to picture mentally is that most of the input domains of even
simple problems have high dimensional spaces associated with them. A
hyperplane is defined to be a surface which lives in an $n$ dimensional
space. The mathematics behind these algorithms is based simply on
solving linear equations, which most people learn in high school
algebra.

Local linear techniques have been used almost exclusively in the past to
analyze time series \[Farmer\]. When analyzing a time series, the idea
is that the nearest neighbors contain the most information relative to
the data point in question. This intuition has been proven by experiment
in a sense that the best prediction methods to date have been local
linear techniques and back propagation. There is still debate focused on
which technique is better \[Farmer, Lapedes\]. In other words, both
techniques have performed about the same on a given time series.

A time series is a set of data points with some arbitrary measure of
time on the x axis and the value at that point of time on the y axis.
Examples of time series include the daily prices of a particular stock,
sun spots, and Las Cruces weather temperatures in 1989 on a daily basis.

## Local Linear Algorithms

There are many different algorithms which are derivatives of the local
linear method. I have chosen to analyze three of these methods simply to
show that the idea of nearest neighbors are significant from an
information theoretic point of view. The only difference between the
following three algorithms is the method in which singularities are
resolved.

### Local Linear

The easiest way to see how this algorithm works is to step through a
very simple example in three dimensions. Since we are dealing with
binary encoded data, there are only eight ways to represent three
dimensional data. Lets assume that seven of the eight possible
representations are available. They are :

::: center
+:-----+:----+:----+:----+:------:+:----------------:+
| Case | Input           | Output | Hamming Distance |
+------+-----+-----+-----+--------+------------------+
| 0\.  | 0   | 0   | 0   | 0      | 1                |
+------+-----+-----+-----+--------+------------------+
| 1\.  | 0   | 0   | 1   | 0      | 2                |
+------+-----+-----+-----+--------+------------------+
| 2\.  | 0   | 1   | 1   | 1      | 1                |
+------+-----+-----+-----+--------+------------------+
| 3\.  | 1   | 0   | 0   | 0      | 2                |
+------+-----+-----+-----+--------+------------------+
| 4\.  | 1   | 0   | 1   | 0      | 3                |
+------+-----+-----+-----+--------+------------------+
| 5\.  | 1   | 1   | 0   | 1      | 1                |
+------+-----+-----+-----+--------+------------------+
| 6\.  | 1   | 1   | 1   | 1      | 2                |
+------+-----+-----+-----+--------+------------------+
:::

The above function represents the idea of **outputting the middle bit
position**. The case that will be generalized on is $(0, 1,
0)$ which is not in the training set.

The idea behind learning algorithms is to train itself on a subset of
the data and then to generalize to the missing pieces. The missing piece
in this puzzle is the the question (0 1 0). The correct answer to this
question is (1), which is the middle bit position of the input space.

The first thing the algorithm does is determine the hamming distance
between the question which is (0 1 0) and the other inputs. Note the
hamming distances between the question and the other neighbors in the
input space in the above table.

After calculating the hamming distances, the distances are ordered
according to the hamming distance to the question. Points that have
distances closer to the question are more important than points further
away. With this in mind the following ordering is calculated (5 2 0 6 3
1 4). Note that although some of the distances are the same, I just
randomly start from the bottom and go up the list.

The number of significant points that are used to calculate the simplex
is the number of input dimensions plus one. So in this particular case I
use 3 + 1 = 4 points in the simplex. The four points in the simplex are
just simply the first four points in the above list. After determining
the points in the simplex, I solve the set of four equations and four
unknowns.

\(5\) $1w + 1x + 0y + z = 1$

\(2\) $0w + 1x + 1y + z = 1$

\(0\) $0w + 0x + 0y + z = 0$

\(6\) $1w + 1x + 1y + z = 1$

The values for the variables are as follows :

w = 0, x = 1, y = 0, z = 0

Then plug into the equation which is not part of training set.

$0w + 1x + 0y + z =$

$0 + 1 + 0 + 0 = 1$

So, as to be expected the answer is one (1)\...

After solving these equations one of two things can happen. First, I can
get back a unique solution to this set of equations and therefore output
an answer to the question. Which is what happened with the above
example. However, in a lot of cases the four equations are not
independent and therefore the algorithm returns the fact that it has
found a singularity. If this happens, then the local linear algorithm
simply goes to the next nearest point and solves the equations again. It
does this until a unique solution is found.

### Herbie II

The original Herbie algorithm was developed by David Wolpert in an
attempt to come up with a quick learning method that uses local linear
ideas. After using his algorithm for awhile, I came up with a derivative
of Herbie which is suitable for simple binary encoded problems. Out of
respect for David Wolpert, I decided to call my algorithm Herbie II. For
a detailed description of the original Herbie algorithm see Wolpert
\[1990\] *"A Benchmark for How Well Neural Nets Generalize"*.

The only difference between the above algorithm, *Local Linear*, and the
Herbie algorithm is what happens if a singularity is found after solving
the set of independent equations. In the *Local Linear* algorithm the
next nearest neighbor was chosen and replaced the point furthest away in
the current equations. The new set of equations are then solved for a
unique set of coefficients.

The herbie algorithm takes a slightly different approach if a
singularity is found initially. It also throws away the furthest point
just like local linear, but instead of taking the next closest point, it
creates a new point which lies on the normal to the hyperplane. After
solving the set of linear equations, if there is still a singularity
then it uses an algorithm called *Weighted Averaging* to find a
solution.

### Weighted Averaging

This technique is used as the final step in the *Herbie algorithm*.
However, it can also be used as a stand alone learning technique. In the
case of binary encoded problems, this algorithm does not perform as well
as the local linear method or *Herbie*; however, for predicting time
series this algorithm is a very viable technique.

The example used to explain this technique is exactly the same example
that was used in section 3.1.1. The algorithm is based on the following
two equations. Note that $i$ is the index of a particular point based on
its hamming distance from the question. So, a point whose index value is
$0$ is the point which is closest to the question, and a point whose
index value is $1$ is the point which is second closest to the question.
The number of points in the simplex equals $N$ which is the number of
input dimensions plus one.

$$X = {\sum_{i = 0}^N} {output[i] \over
hammingdistance[i]}$$

$$Y = {\sum_{i = 0}^N} {1 \over hammingdistance[i]}$$

and the solution to the problem is

$$answer = {X \over Y}$$

So, in the case of the example in section 3.1.1 the hamming distance
indexes are $(5, 2, 0, 6, 3, 1, 4)$. Only four of the seven points are
used since the number of input dimensions is three.

::: center
+:-----+:----+:----+:----+:------:+:----------------:+
| Case | Input           | Output | Hamming Distance |
+------+-----+-----+-----+--------+------------------+
| 0\.  | 0   | 0   | 0   | 0      | 1                |
+------+-----+-----+-----+--------+------------------+
| 1\.  | 0   | 0   | 1   | 0      | 2                |
+------+-----+-----+-----+--------+------------------+
| 2\.  | 0   | 1   | 1   | 1      | 1                |
+------+-----+-----+-----+--------+------------------+
| 3\.  | 1   | 0   | 0   | 0      | 2                |
+------+-----+-----+-----+--------+------------------+
| 4\.  | 1   | 0   | 1   | 0      | 3                |
+------+-----+-----+-----+--------+------------------+
| 5\.  | 1   | 1   | 0   | 1      | 1                |
+------+-----+-----+-----+--------+------------------+
| 6\.  | 1   | 1   | 1   | 1      | 2                |
+------+-----+-----+-----+--------+------------------+
:::

$$X = {1 \over 1} + {1 \over 1} + {0 \over 1} + {1 \over 2} = 2.5$$

$$Y = {1 \over 1} + {1 \over 1} + { 1 \over 1} + {1 \over 2} = 3.5$$

and the answer is $$answer = {X \over Y} = .71$$

rounding gives the correct answer of $1$.
