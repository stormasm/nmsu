# Introduction

The purpose of this paper is to compare and contrast two types of
learning algorithms and how they perform on simple binary encoded
problems. The first type of learning algorithm is a local linear
technique based on nearest neighbors in a multi dimensional simplex.
Three different algorithms based on this idea will be analyzed. The
second type of learning algorithm will be the traditional back
propagation. Simple binary encoded examples are chosen in order to to
understand the techniques clearly, rather than getting confused by
complicated learning domains. Emphasis will be placed on showing
empirically how back propagation and local linear methods are both doing
surface fitting. Since the experimental results for both algorithms are
basically the same, this will also delineate the fact that both
techniques are similar in *learning abilities*.

## What is a Learning Algorithm ?

The term learning algorithm was coined by AI researchers in the 1960's
hoping to get computer programs to perform simple human tasks. Since
that time, many different types of algorithms have become popular. In
the 1960's Newell and Simon worked on the General Problem Solver. In the
1970's expert systems were used as a research tool and then further
developed into marketable products in the 1980's. In the past five
years, a third wave of algorithms based on *connectionism* or neural
networks have been popularized.

It has not been made clear in the literature that the *connectionist*
algorithms are based upon traditional function approximation or surface
fitting techniques. Given a set of points on the x - y axis, a learning
algorithm can use many different types of methods to come up with the
best fit. They include least squares, polynomial interpolation, splines,
fourier analysis, back propagation and local linear methods. The
technique that works best is based upon how well the function makes
predictions or generalizations.

Given a set of fifty points on the x - y axis, one of the above methods
will come up with the best function. That function is the one which most
accurately predicts the next ten points which were not part of the
training set. This method of generalization can also be called learning.

In this paper, the domain and range of the functions are not part of the
x - y axis, but rather they are located on the boolean hypercube.
Problems which are located on the hypercube are sometimes called
discretized problems. These are opposite from analog or continuous
problems which most function approximations are used to dealing with.
The following chapters outline two main types of function approximators,
namely back propagation and local linear methods.

## Previous Work

The idea of local linear methods was first introduced by Stephen
Omohundro \[1987\] in a paper entitled \"Efficient Algorithms with
Neural Network Behavior\". The idea of using nearest neighbors for
pattern classification was introduced by Cover \[1967\]. Omohundro's
paper is a landmark paper and should be the first reference read by
anyone interested in further reading on this subject. In his paper he
emphasizes the point that much more efficient learning algorithms than
back propagation are available, and describes them from a theoretical
point of view. He addresses a much larger question than just the
algorithm efficiency. Omohundro tries to group continuous and discrete
problems into classes of problems and then justifies why those types of
problems are best suited for a particular algorithm. One crucial point
in his paper deals with the significance of pseudo random number
generators and how they play a very important role in the modern day
stochastic simulations. The one minor criticism of Omohundro's work is
the fact that he does not actually run any experiments to test his
ideas.

Farmer and Sidorowich \[1988\] expand on Omohundro's ideas and discuss
prediction of chaotic time series. Lapedes and Farber \[1988\] study the
same times series as Farmer but use neural networks to analyze the data.
No specific comparisons of the two techniques are outlined in either
paper but the reader could certainly come up with a better intuitive
feel of analyzing continuous data using these methods.

David Wolpert \[1989\] is the first person to actually compare both back
propagation and local linear methods on discrete problems. In this
paper, he runs the local linear methods on a set of problems and then
compares them to the method of back propagation. Wolpert \[1990b\] is an
excellent theoretical introduction to the ideas of local linear methods.
Wolpert \[1990a\] compares the Sejnowski and Rosenberg \[1987\] work on
Net Talk, \"Parallel Networks that Learn to Pronounce English text\"
against local linear methods and shows that local linear methods
actually do better than back propagation.

In this paper, I expand on the ideas of Wolpert's work by choosing new
binary encoded problems and verify empirically that both back
propagation and local linear methods perform about the same. It is
hopefull that further research in this area will clarify which methods
are appropriate for a certain class of discrete problems.
