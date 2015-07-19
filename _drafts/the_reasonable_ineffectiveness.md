Let's start with a very simple task. Write a program that, when given a 2x2 matrix A and a 2 element vector b, will use gradient descent
to solve the linear equation Ax=b. Barring deficiencies in calc and linear algebra, most programmers can feel comfortable that they can
approach this problem, even if they don't know how.

Now comes the coda, verify it correctly implements the gradient descent algorithm. Strangely, we can't do this. Since the seminal work of
Turing's solution to Entscheidungsproblem, we struggle to come to terms with the honest fact that we have no idea if our programs work. 
Even for gradient descent, the proof of convergence of the algorithm requires calculus, and one cannot reasonably show their program exactly
meets the specification. 
