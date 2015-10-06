---
layout : post
title  : Markov Chain Monte Carlo simulation in 10 Minutes
snip   : When all else fails... simulate everything
---

##Markov Chain Monte Carlo simulation in 10 Minutes  

###What is a random variable?

A random variable can have many different formal definitions, but let's avoid technicalities for the moment and give an intuitive
definition:

A random variable is a variable that can be any one of the values in a given set S. At any time we can "observe" the variable. At that point,
it will **be** some value in the set. Before we observe which value it is, we have a function that when given some value x in S, it will
tell us the probability of seeing x once we reveal the random variable*.

Here's one. It simply is a uniform random variable, where every 3 second we observe it's value.

<iframe width="100%" height="150" src="//jsfiddle.net/jrab227/4fne66db/embedded/result,js,html" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

The non-deterministic nature of random variables makes them widely studied area, and their applications are everywhere. Having an idea of what
may happen in the future given data from today is essential in our daily lives so naturally random variables are a perfect way to model the
future with information today. Of course models aren't perfect, but something is always better than nothing. 

###What is a Markov Chain?

A Markov Chain is a slight extension of a random variable. Again avoiding technicalities, a markov chain is simply a sequence of random variables.
We observe a variable, then observe the next variable in order, one by one. What makes them special is that the probabilities can be 
"updated" depending on the observed value of the previous random variable. For a really good introductory explanation on markov chains,
[check out this visual introduction if you want a great explaination.](http://setosa.io/blog/2014/07/26/markov-chains/) 

For an even better explaination, read Yueng [1].

###Metropolis-Hastings and simulating a Random Variable

Have you ever wondered how exactly random numbers are generated in your favorite language? 
Most have some support for generating samples from a uniform distribution. Javascript specifically has Math.random() 
to help with generating samples that are between 0 and 1, but how do we generate a list of numbers that appear as if
they are sampled from from say, a normal distribution? This is where the Metropolis-Hastings algorithm comes in.

Simply put, if we have a target distribution we want to sample from, and some way to generate samples from a uniform distribution,
the Metropolis-Hastings algorithm gives us a way to generate samples from the target distribution. We'll work with a simple standard
normal distribution. The probability function is below.

<iframe width="100%" height="130" src="//jsfiddle.net/jrab227/ansgp4jd/1/embedded/js" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

Now again, this is the problem, we want *samples* from this distribution, essentially a set of numbers that look like they've come from
this particular distribution. This is the algorithm of Metropolis-Hastings:

<iframe width="100%" height="220" src="//jsfiddle.net/jrab227/qdzof63d/1/embedded/js" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

After given a way to generate a random uniform variable, to generate a value in the target distribution, we:

1. Create some new state from a given state using any way we like**.
2. Compute the odds of the system being in state B or A.
3. Generate a random variable that is uniform, and if it's less than the odds of B or A, move to the new state. Otherwise, stay in the state.

The intuition behind it is this: lets say we have a state A and a state B where the probability of oberving A is 2/3 and the probability
of observing B is 1/3. If we are in state B, the odds are 2:1. The point is, the system should be in state A twice as much as B, so any
algorithm that generates observations of a random variable defined with these probabilities should account for this. The accounting is done
in the transition odds. In the reverse, where we are in state A and want to move to state B, the odds are 1:2, hence we should move from A to B 1/2 of the time. The transitions odds in both directions essentially make the system stay in state A twice as much as state B. The
beauty of the Metropolis-Hastings algorithm is that in a very simple program, we can meet these requirements *and* sample efficiently.

Now finally, we take a million samples using the Metropolis-Hastings Algorithm, taking a million samples. In it, we make the next state
choice simply by going left or right from the current state by a small distance. The plot is below.

Does it look Normal enough?

<iframe width="100%" height="450" src="//jsfiddle.net/jrab227/r8cn8jef/1/embedded/result,js" allowfullscreen="allowfullscreen" frameborder="0"></iframe>

###Further Reading

[1]. Yueng, Information Theory and Network Coding. [Link](http://www.amazon.com/Information-Theory-Network-Coding-Technology/dp/0387792333)

[2]. Casella and Berger, Statistical Inference. [Link](http://www.amazon.com/Statistical-Inference-George-Casella/dp/0534243126)

[3]. Chib and Greenburg, Understanding Metropolis-Hastings [Link](http://biostat.jhsph.edu/~mmccall/articles/chib_1995.pdf)

\* There are actually mathematical details into the definition of a random variable. IANAM (I am not a mathematician), but there
are topological issues with the domain of probability functions, along with satisfying conditions known as Komolgorov
axioms. There's actually a nice definition in the first few chapters of Casella and Berger [2] but even then, the formal definition has some quirks that 
only mathematicians need to deal with in proving theorems.

** This isn't entirely true. You actually need a condition that, when going from state A to B, the probability of going from A to B is the
same as going from B to A. There is a correction factor mentioned in Chib and Greenburg [3] that is multiplied by the transition odds, but for our case, 
since this condition is met, the factor is just 1. 
