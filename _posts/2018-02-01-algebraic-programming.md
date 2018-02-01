---
layout : post
title  : Algebras and Declarative Programming 
snip   : Using what you're used to, the way you know how
---

Start by explaining complex systems of code with nested structure.
Show some examples of algebras, and show how many constructs could be algebraic.
Explain how a better design is to simplify code into layers that
manipulate structures in a linear fashion, like algebras.

### What *is* declarative programming?

Explain how no one really knows what declarative vs imperative programming is.
Languages are all imperative by nature.
All programs have state.

### Imperative vs Declarative Is A Matter of Style

### Monoids, Monads, Algebras...

### Monoidal Functions

### Error Handling, Algebraicly (Well... Monadically)

### Thinking Algebraically In Practice

While all of this is nice, the reality is most software doesn't initially scream
amenability
to an algebraic way of thinking. Software engineers are typically given user stories like this...

** A User should be able to log in with their email ** 

It's very hard upon first look to determine how to design code for a particular feature, when stories are centered by
the user's perspective, which is invariably the "goal" of the code.
