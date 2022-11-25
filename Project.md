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
