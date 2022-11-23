#####  Abstract
Life is like a bivouac filled with randomness and adventure. In this random aspect of life, we come across some ordinary, rather home-do-able events that make things fascinating and brings our minds to thoughts of action which speak louder than words. Keeping these things in mind, a throw of a die is probably one of the first experiments as we have learned in probability. The things we have learned are more theoretical than practical perspectives. To enlighten upon the practical aspect of this turn, we must bring in some verification to some generalized aspects and notions. This verification is done with the help of simulation. We know that each probabilistic problem has a journey on its own. We have tried our best to highlight most of it along with simulation and have tried to display a visualization of some engrossing features each problem consists of. The use of the Markov Chain in solving problems has been a real pleasure to make things even more interesting.

### Part 1: Introduction
On constant thought of action, a throw of a die is a random event from a probabilistic aspect. On the hint of such randomness there are some basic yet interesting problems and extensions that can be raised as we constantly work on problems related to this. Let's answer some questions howsoever to work through.
######  Note-
We set the seed of our simulation codes at 20 so as to have some sort of reproducibility in our results
```
set.seed(20)
```

### Part 2: The Questions and their Treatments
####  1.  On an average, how many times must a 6-sided die be rolled until a 6 turns up?
Seems like an easy enough problem, isn't it?
In other words we are asked to find expected no. of rolls until a 6 appear.
Then probability that $X=1$ is $\frac{1}{6}$, $X=2$ is $\frac{5}{6}\times\frac{1}{6}=\frac{5}{36}$.
In general prob that $X=k$ is
$$P\left(X=k\right)=\left(\frac{5}{6}\right)^{k-1}\frac{1}{6}\quad,k=1,2,\ldots$$
Since in order for $x$ to be $k$, there must be $(k-1)$ rolls which can be any of the numbers 1 to 5, and then 6, which appears with probability $\frac{1}{6}$.
We seek the expectation of $X$.
