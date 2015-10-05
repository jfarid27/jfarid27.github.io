---
layout : post
title  : Markov Chain Monte Carlo simulation in 10 Minutes
snip   : When all else fails... simulate everything
---

##What is a random variable?

A random variable can have many different formal definitions, but let's avoid technicalities for the moment and give an intuitive
definition:

A random variable is a variable that can be any one of the values in a given set S. At any time we can "observe" the variable. At that point,
it will **be** some value in the set. Before we observe which value it is, we have a function that when given some value x in S, it will
tell us the probability of seeing x once we reveal the random variable*.

Here's one. It simply is a uniform random variable, where every 3 second we observe it's value.

<iframe width="100%" height="200" src="//jsfiddle.net/jrab227/4fne66db/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

The non-deterministic nature of random variables makes them widely studied area, and their applications are everywhere. Having an idea of what
may happen in the future given data from today is essential in our daily lives so naturally random variables are a perfect way to model the
future with information today. Of course models aren't perfect, but something is always better than nothing. 

##What is a Markov Chain?

A Markov Chain is a slight extension of a random variable. Again avoiding technicalities, a markov chain is simply a sequence of random variables.
We observe a variable, then observe the next variable in order, one by one. What makes them special is that the probabilities can be 
"updated" depending on the observed value of the previous random variable. For a really good introductory explanation on markov chains,
[check out this visual introduction if you want a great explaination.](http://setosa.io/blog/2014/07/26/markov-chains/) 

##Metropolis-Hastings and simulating a Random Variable

Have you ever wondered how exactly random numbers are generated in your favorite language? 
Most have some support for generating samples from a uniform distribution. Javascript specifically has Math.random() 
to help with generating samples that are between 0 and 1, but how do we generate a list of numbers that appear as if
they are sampled from from say, a normal distribution? This is where the Metropolis-Hastings algorithm comes in.

Simply put, if we have a target distribution we want to sample from, and some way to generate samples from a uniform distribution,
the Metropolis-Hastings algorithm gives us a way to generate samples from the target distribution. We'll work with a simple standard
normal distribution. The probability function is below.

<iframe width="100%" height="100" src="//jsfiddle.net/jrab227/ansgp4jd/1/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Now again, this is the problem, we want *samples* from this distribution, essentially a set of numbers that look like they've come from
this particular distribution. This is the algorithm of Metropolis-Hastings:

<iframe width="100%" height="220" src="//jsfiddle.net/jrab227/qdzof63d/1/embedded/" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

After given a way to generate a random uniform variable, to generate a value in the target distribution, we:

1. Create some new state from a given state using any way we like**.
2. Compute the odds of the system being in state B or A.
3. Generate a random variable that is uniform, and if it's less than the odds of B or A, move to the new state. Otherwise, stay in the state.

\* There are actually mathematical details into the definition of a random variable. IANAM (I am not a mathematician), but I see 
a random variable as a set S and a function F from the space of Borel sets of S to real numbers that are consistent with Komolgorov
axioms. There's actually a nice definition in the first few chapters of C&B[2] but even then, the formal definition has some quirks that only mathematicians need to deal with in proving theorems.

** This isn't entirely true. You actually need a condition that, when going from state A to B, the probability of going from A to B is the
same as going from B to A. There is a correction factor mentioned in C&G[3] that is multiplied by the transition odds, but for our case, 
since this condition is met, the factor is just 1. 

<iframe height="320" width="50%" frameborder="0" seamless="seamless" scrolling="no" src="https://plot.ly/~jrab227/35/"> </iframe>

##Further Reading

[1]. Yueng, Information Theory and Network Coding. [Link](http://www.amazon.com/Information-Theory-Network-Coding-Technology/dp/0387792333)
[2]. Casella and Berger, Statistical Inference. [Link](http://www.amazon.com/Statistical-Inference-George-Casella/dp/0534243126)
[3]. Chib and Greenburg, Understanding Metropolis-Hastings [Link](http://biostat.jhsph.edu/~mmccall/articles/chib_1995.pdf)

