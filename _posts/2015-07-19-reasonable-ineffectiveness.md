---
layout : post
title  : The Reasonable Ineffectiveness of Programming 
snip   : ... or why we have jobs in the first place.
---

Let's start with a very simple task. Write a program that, when given a 2x2 matrix A and a 2 element vector b, will use gradient descent
to solve the linear equation Ax=b. Barring deficiencies in calc and linear algebra, most programmers can feel comfortable that they can
approach this problem, even if they don't know how.

Now comes the coda, verify it correctly implements the gradient descent algorithm. Strangely, we can't do this. Since the seminal work of
Turing's solution to Entscheidungsproblem, we struggle to come to terms with the honest fact that we have no idea if our programs work. 
Even for gradient descent, the proof of convergence of the algorithm requires calculus, and one cannot reasonably show their program exactly
meets the specification. 

At best, a statement about a few points in the space of 2x2 matrices is all we can muster. A check that Ax=0 returns x=0 is an important check,
but how can we still say our program is correct on just a finite set of inputs? The space of 2x2 matrices is worse than the reals*. Simply put,
any statement about an infinite span of inputs, using only one point seems unsound, and we certainly cannot check all inputs. In practice, these
scenario tests on finite points are little more than reasoning checks for programmers and can barely be held as effective checks for specifications.
The central task of a programmer, to not only devise programs that meet specifications, but prove that they are consistent with them, seems a lost
cause.

Type theory provides little resolution to the task, as blurring proofs of propositions and programs only reiterates the difficulty of creating a
proof of a specification. A programmers task to prove a program correct is equal to the task of a mathematician proving a theorem. Both camps
are faced with the reality that in the space of all possible programs and theorems, proofs are not guaranteed. What is interesting is the tools
both use to gain some insight into specifications to answer their dual questions, "Is my program correct?"

Abstraction, being the basic tool of the trade is easy to use, but extremely difficult to wield, as it's correct usage is entirely hinged upon
the users decisions on what to abstract. It's logical form, the implication, hardly should appease the programmer if the abstraction is made too
loosely or too rigid. Building upon subcomponents assumed correct is unweildy territory, as a break in a previous assumption can cascade failures
throughout a program. While useful in its own right as a tool to help prove programs correct, abstraction can be both useful, and a massive problem
when code systems become large. 

Beyond abstraction, a multitude of tools exist to help programmers prove programs correct. Recursion, along with it's logical form, proof by induction,
again proves useful as a way to prove programs correct. It's weakness, a dependency on well-typed data structures, shows its use can also be difficult,
as it is quite difficult to show a well-typed data structure has a base. Even further, path actions, similar to functors in category theory, offer some
help in proving statements correct by mapping dependent types to other similar dependent types, provided the programmer can produce a map. There are
other forms as well in homotopy type theory that help the task, but even in this theory, axioms are taken that are central to the entire system,
univalence being one of them.

In the massive space of programs that can exist, few can be proven correct. Large swaths of program systems
are used without any real indication that they are correct. The nature of programs and proving theorems is largely a search for a needle in a haystack
and it should be no surprise that failures in systems occur. An inconsisteny in a large theoretical system is just as expected as a bug in a code.
In some sense, while we can guarantee the correctness of some programs, they are mostly ineffective at solving problems, given the ability to create
problems which programming cannot solve. On both sides, constant corrections and assumptions are made in an effort to maintain these large systems, but
to what extent? Why should a large system ever be correct when it's underlying components may be broken?
