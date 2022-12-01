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
```math
\begin{align}
E\left(X\right) & =\sum_{n=1}^{\infty}nP\left(x=n\right)\\
\Rightarrow E\left(X\right) & =\sum_{n=1}^{\infty}n\left(\frac{5}{6}\right)^{n-1}\cdot\frac{1}{6}=\frac{6}{5}\cdot\frac{1}{6}\sum_{n=1}^{\infty}n\left(\frac{5}{6}\right)^{n}\\
 & =\frac{1}{5}\sum_{n=1}^{\infty}n\left(\frac{5}{6}\right)^{n}\quad\text{ Which is an AGP series }\\
 & =\frac{1}{5}\left(\frac{\frac{5}{6}}{1-\left(\frac{5}{6}\right)^{2}}\right)\\
 & =\frac{1}{5}\times\frac{5}{6}\times\frac{36}{1}\\
 & =6
\end{align}
```
Thus on an average it takes 6 throws of a die before a 6 appears.
######  Simulation
We do the simulation in the following manner:
```
rolls<-function()
{
	x<-sample(1:6,1)
	i=1
	while(x!=6)
	{
		x<-sample(1:6,1)
		i=i+1
	}
	return(i)
}
mean(replicate(10000,rolls()))
```
Upon doing the simulation, we get the value as: `6.0523`. Taking the mean from 5 times the above calculation, we also do a simulation to get a better estimate:
```
mean(replicate(5,mean(replicate(10000,rolls()))))
```
This returns a value of `6.018`
######  Conclusion
We have observed by using simulation that the expected value of rolling a die until a 6 turns up is almost equal to 6. This verifies the probabilistic approach we used to find an answer to this question. The more the sample, the closer will be the result of the simulation to the number 6, as we found out in our comparative simulation.
####  2.	On an average, how many times must a 6-sided die be rolled until a 6 turns up twice a row?
We use recurrence relation to solve this, Let $E(X)$ be expected
no. of rolls. When we start rolling, we expect, on average 6 rolls
until a 6 shows up. Once that happens, there is a $\frac{1}{6}$ chance
we will roll once more and a $\frac{5}{6}$ chance that we will be
effectively starting all over again, and so have as many starting
all over again, and so have as many additional rolls as when we started,
we say,
```math
\begin{align}
E\left(X\right) & =6+\frac{1}{6}+\frac{5}{6}\left(E\left(X\right)+1\right)\\
\implies\frac{1}{6}E\left(X\right) & =6+\frac{1}{6}+\frac{5}{6}\\
\implies E\left(X\right) & =42
\end{align}
```
Thus, on an average 42 is no. of times needed for a dice to be rolled until 6 appears twice in a row.
######	Simulation
We do the simulation in the following manner:
```
rolls<-function()
{
	j=0
	x<-sample(1:6,1)
	i=1
	if(x==6)
	{
		j=1
		x<-sample(1:6,1)
		i=i+1
		if(x!=6) j=0
	}
	while(j!=1)
	{
		x<-sample(1:6,1)
		i=i+1
		if(x==6)
		{
			j=1
			x<-sample(1:6,1)
			i=i+1
			if(x!=6) j=0
		}
	}
	return(i)
}
mean(replicate(10000,rolls()))
```
Upon running this, we found the value to be: `41.5374`.Taking the mean from 5 times the above calculation, we also do a simulation to get a better estimate:
```
mean(replicate(5,mean(replicate(10000,rolls()))))
```
This returns the value: `42.32468`
######	Conclusion
We have observed by using simulation that the expected value of rolling
a die until a 6 turns up twice in a row is almost equal to 42. This
verifies the probabilistic approach we used to find an answer to this
question. The more the sample, the closer will be the result of the
simulation to the number 42, as we found out in our comparative simulation.
####	3.	On average, how many times must a 6-sided die be rolled until the sequence 65 appears (that is a 6 followed by a 5)?
In this problem, once we roll a 6 there are 3 possibilities:
- We roll a 5
- We roll a 6
- We start over again

We again use recursion, but we will have two simultaneous equations.
Let $E$ be the expected number of rolls until 65 and let $E_{6}$
be the expected number of rolls until 65 when we start with a rolled
6. Then
```math
\begin{align}
E_{6} & =\frac{1}{6}\left(E_{6}+1\right)+\frac{4}{6}\left(E+1\right)+\frac{1}{6}\times1\\
E & =\frac{1}{6}\left(E_{6}+1\right)+\frac{5}{6}\left(E+1\right)
\end{align}
```
On solving both, we have
$$E=36\;E_{6}=30$$
######	Simulation
We do the simulation in the following manner:
```
rolls<-function()
{
	j=0
	x<-sample(1:6,1)
	i=1
	while(x==6)
	{
		j=1
		x<-sample(1:6,1)
		i=i+1
		if(x!=5) j=0
	}
	while(j!=1)
	{
		x<-sample(1:6,1)
		i=i+1
		while(x==6)
		{
			j=1
			x<-sample(1:6,1)
			i=i+1
			if(x!=5) j=0
		}
	}
	return(i)
}
mean(replicate(10000,rolls()))
```
Upon running this, we found the value to be: `35.7654`.Taking the mean from 5 times the above calculation, we also do a simulation to get a better estimate:
```
mean(replicate(5,mean(replicate(10000,rolls()))))
```
This returns the value: `36.07392`
######	Corollary: It takes lesser rolls on an average to see a 6 followed by a 5 than for 6 followed by 6.
######	Conclusion
We have observed by using simulation that the expected value of rolling a die until a 6 turns up followed by a 5 is almost equal to 36. This verifies the probabilistic approach we used to find an answer to this question. The more the sample, the closer will be the result of the simulation to the number 36, as we found out in our comparative simulation.
####	4.	On average, how many times must a 6-sided die be rolled until there are two rolls in a row that differ by 1(such as a 2 followed by a 1 or 3, or a 6 followed by a 5)? What if we roll until there are two rolls in a row that differ by no more than 1(so we stop at a repeated roll, too)?
Let $E$ be the expected no. of rolls. Let $E_{i}$ be the expected
no. of rolls after rolling an $i$ (not following a roll of $i-1$
or $i+1$). Then, we have
$$E=1+\frac{1}{6}\left(E_{1}+E_{2}+E_{3}+E_{4}+E_{5}+E_{6}\right)$$
By symmetry, we have $E_{1}=E_{6},\;E_{2}=E_{5},\;E_{3}=E_{4}$ and
thus
$$E=1+\frac{2}{6}\left(E_{1}+E_{2}+E_{3}\right)$$
We can also right $E_{1}$as $E_{1}=1+\frac{2}{6}E_{1}+\frac{1}{6}E_{2}+\frac{2}{6}E_{3}$.
Since there will be an additional roll, there is a $\frac{1}{6}$
chance that this will be the last roll (i.e. we roll a 2) and five
other possibilities are equally likely. Similarly, $E_{2}=1+\frac{1}{6}E_{1}+\frac{2}{6}E_{2}+\frac{1}{6}E_{3}$
and $E_{3}=1+\frac{2}{6}E_{1}+\frac{1}{6}E_{2}+\frac{1}{6}E_{3}$.
Thus, after solving, we get,
$$E_{1}=\frac{70}{17},\;E_{2}=\frac{58}{17},\;E_{3}=\frac{60}{17}$$
Thus, we get that,
$$E=1+\frac{1}{3}\times\left(\frac{70+58+60}{17}\right)=\frac{239}{51}=4.6862$$
######	Simulation
We do the simulation in the following manner:
```
rolls<-function()
{
	x<-sample(1:6,1);y<-sample(1:6,1)
	i=2
	while(abs(x-y)!=1)
	{
		x<-y;y<-sample(1:6,1)
		i=i+1
	}
return(i)
}
mean(replicate(10000,rolls()))
```
Upon running this, we found the value to be: `4.702`. Taking the mean from 5 times the above calculation, we also do a simulation to get a better estimate:
```
mean(replicate(5,mean(replicate(10000,rolls()))))
```
This returns the value: `4.69556`
######	Conclusion for first part
We have observed by using simulation that the expected value of rolling
a die until there are two rolls in a row that differ by 1 is almost
equal to 4.6862. This verifies the probabilistic approach we used
to find an answer to this question. The more the sample, the closer
will be the result of the simulation to the number 36, as we found
out in our comparative simulation.

If we stop when we have a repeated roll too, a similar situation arises.
Defining $E,E_{1},E_{2},E_{3}$ as same, we have
```math
\begin{align}E & =1+\frac{2}{6}\left(E_{1}+E_{2}+E_{3}\right)\\
E_{1} & =1+\frac{1}{6}E_{1}+\frac{1}{6}E_{2}+\frac{2}{6}E_{3}\\
E_{2} & =1+\frac{1}{6}E_{1}+\frac{1}{6}E_{2}+\frac{1}{6}E_{3}\\
E_{3} & =1+\frac{2}{6}E_{1}+\frac{1}{6}E_{2}
\end{align}
```
Solving, we get,
```math
\begin{align}
E_{1} & =\frac{288}{115},\;E_{2}=\frac{246}{115},\;E_{3}=\frac{252}{115}\\
E & =1+\frac{1}{3}\left(\frac{288+246+252}{115}\right)=\frac{377}{115}=3.278
\end{align}
```
######	Simulation
We do the simulation in the following manner:
```
rolls<-function()
{
	x<-sample(1:6,1);y<-sample(1:6,1)
	i=2
	while(abs(x-y)>1)
	{
		x<-y;y<-sample(1:6,1)
		i=i+1
	}
return(i)
}
mean(replicate(10000,rolls()))
```
Upon running this, we found the value to be: `3.247`. Taking the mean from 5 times the above calculation, we also do a simulation to get a better estimate:
```
mean(replicate(5,mean(replicate(10000,rolls()))))
```
This returns the value: `3.29216`
######	Conclusion for second part
We have observed by using simulation that the expected value of rolling a die until there are two rolls in a row that differ by at most 1 is almost equal to 3.278. This verifies the probabilistic approach we used to find an answer to this question. The more the sample, the closer will be the result of the simulation to the number 3.278, as we found out in our comparative simulation.
######	Corollary: The expected values of rolls until there are two rolls in a row that differ by 1 is greater than the expected number of rolls until there are two rolls in a row that differ by no more than 1
