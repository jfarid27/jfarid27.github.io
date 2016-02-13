---
layout : post
title  : Network Properties and Rice's Theorem 
snip   : Why we can't decide whether a network flash-crashes
---

I was recently shown [a paper by Majdandzic, Stanley et. al](http://polymer.bu.edu/hes/articles/mpbkhs14.pdf) that describes some interesting dynamical
behaviors of complex networks. This particular paper describes spontaneous massive system changes colloquially known as "flash-crashes", that
describe large system jumps even though on short time scales, the system appears stable. While I've only discussed minor details with others, I'm sure
there is no reasonable way to determine at a glance if a particular network topology and evolution scheme has, not only flash-crash properties, but
any non-trivial property. This is related to Rice's Theorem, since it asserts there is no way to determine if, for any program, whether the program has
or does not have a non-trivial property. The statements below are of the style seen in the basic, "Hello World" tester in Ullman et. al's Automata Theory,
Languages, and Computation. There is a distinction between "trivial" and "non-trivial" properties, but this is too advanced and misses the point
since a network being a flash-crash network is clearly non-trivial.

For brevity, call a network and evolution scheme a "network" for short, and call a program that when run with arguments, simulates the network simply a "simulation". It's reasonable to assume if we could tell whether a network has a property, we can tell whether the simulation which encodes a network has a property, so below is a non-formal proof for the simulation of networks.

To show there is no way to determine whether a simulation has a property P, assume a special program exists that can decide when given a simulation and it's argument set,
whether it has property P, and emits "Yes" or "No" whether or not the simulation has the property.
Refer to this network and scheme as N. Refer to the special program as O. Now modify O to emit a known simulation with property P, called A, instead of "No".
So this modified program, when given a simulation without the property P, emits A and otherwise "Yes". Refer to this modified program as O_1.
Now further modify the program so that instead of being given a simulation and argument set, receives only a simulation, and calls the simulation with the simulation.
Call this program O_2.

Now, call O_2 with itself, O_2. This operation is O_2(O_2). Assume O_2(O_2) outputs A. Then the internal call O_2(O_2) outputs "Yes" since otherwise, 
it would have A as output. Now assume O_2(O_2) outputs "Yes". Then the internal call O_2(O_2) outputs A, since otherwise, it would have output "Yes" 
as a result. These statements form a paradox. Since it's fairly trivial to modify programs, and network simulations can be found which have property P,
the only available assumption to discharge is that O existed, so O does not exist. This is a contradiction, so no program O can exist.

What's interesting is, P can be any non-trivial property of networks since P wasn't specified. This includes the non-trivial flash-crash property.
Note that this is a diagonalization argument akin to Godel-Turing style proofs of undecidability, meaning there may exist programs that can decide *some*
networks, but this program will fail to decide, as in, will fail to emit either "Yes" or "No" when given some networks, so a search for an all
encompassing program is a waste of time, since one cannot exist.
