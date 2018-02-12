---
layout : post
title  : Algebras and Declarative Programming 
snip   : Using what you're used to, the way you know how
---

In software engineering, numerous colloquial definitions of the designation between imperative and declarative programs exist in regards to the design of
program structures. Formally, the use of the word "imperative" designates languages with state that users of the language can change and manipulate.
By this definition, all modern languages are imperative, since all modern languages have some form of internal state that the program
can manipulate, but previous languages that did not have a separation between the computer's memory and a programs internal state,
even a virtualized internal state, clearly were imperative.

Because of the rise of imperative languages, formally the line between characterizing a language as imperative or declarative is no
longer relevant, and the non-formal definition of the designation of declarative or imperative as the difference between a program that
describes "what" it does rather than "how" it does it reigns, giving the designation a *design* definition rather than a *formal* definition.
This post explores the dichotomy of declarative vs imperative programs, identifying *algebraic* abstractions like Promises, 
EventEmitters, and interfaces like Monads as declarative structures. 

### Algebraic Structures as Declarative

A familiar connection between algebras and Promises exists by connecting ```then``` with ```+```. For example, in the code below,
```getAndTransformData``` is a combination of ```GetData + fetchResponse + transformResponse```. 

~~~ javascript

const fetchResponse = (response) => AsyncFetch(response.data.id)
  .then((innerResponse) => {
    innerResponse.matchingId = response.data.id;
    return innerResponse;
  });

const transformResponse = (response) => {
  response.count + 1 = response.count + 1;
  return response;
};

const getAndTransformData = () => GetData("id").then(fetchResponse).then(transformResponse);
~~~

The code above is familiar to anyone with training in algebras, and can be easily interpreted by other engineers. What is interesting,
is that structurally, the level "above" the handlerFunctions is algebraic, while the level "of" the handlerFunctions is extremely
imperative, manipulating data objects directly. This split between an imperative level that describes "how" things being done, and
an abstraction over the imperative level that describes "what" is being done is common when working with asynchronous code using
Promises, and shows how imperative code can be abstracted to a declarative language.

### Monads are Algebraic (Well, monoidal)

Monads are a useful tool in functional languages as a way to control context and ensure correctness of programs. For example, in Haskell
the Monad interface is described for List objects, and allows programmers to manipulate Lists using an economic set of functions

```haskell
splitNegative x = [-x, x]

translate10 x = [x + 10]

let results = [1, 2, 3] >>= splitNegative >>= translate10
```

Once Again, an engineer can see the dichotomy between an imperative level, describing the manipulations of state, as well as a 
declarative level, describing what is being done to the state without explicitly mentioning the details.

### Algebraic Design Patterns

As the previous code sections show, abstracting imperative code using algebraic design patterns can lead to a declarative design that is
easier to maintain, compose and understand. As a final example, let's look at a common task for Javascript programmers: updating 
multiple nested properties of an object.

```javascript
let user = {
  id: '1',
  email: 'bar@mailinator.com',
  profile: {
    name: 'John Doe',
    phone: '12345',
    favoriteColor: 'blue'
  }
};

user.profile.name = "Sarah Doe";
user.email = "foo@mailinator.com";
user.profile.favoriteColor = 'green';
```

One can build a declarative level abstraction over the actions of updating the object, by describing actions on the object, then
using [an appropriate concatenator of functions](https://lodash.com/docs/4.17.5#flowRight).

```javascript
let user = {
  id: '1',
  email: 'bar@mailinator.com',
  profile: {
    name: 'John Doe',
    phone: '12345',
    favoriteColor: 'blue'
  }
};

const updateName = name => user => {
  user.profile.name = name;
  return user;
};

const updateEmail = email => user => {
  user.email = email;
  return user;
};

const updateFavoriteColor = color => user => {
  user.profile.favoriteColor = color;
  return user;
};

let updatedUser = _.flowRight([
  updateName('Sarah Doe'),
  updateEmail('foo@mailinator.com'),
  updateFavoriteColor('green')
])(user);
```

After realizing a concatenator, one can compose and modify the original application in a straightforward way, and one can see the
design of code is more modular and modifyable than before.

### Consider Algebraic When Writing Code

Unfortunately, many engineers in an Agile system are given tasks described by project managers such as, "As a User, I wish to see my
count of daily logins". When building a system, one cannot see the connections between components well enough to justify building
an abstraction layer, especially when the overall goal of the task is to produce a result and not to observe similarities to other code.
This leads to bloated software, where many components are arguably doing similar things on state which could be compressed into a
single abstraction. On top of this, as teams get large and engineers own feature areas, problems are exacerbated by the reality that
many engineers are writing code that does similar things on state, but are unaware of other engineers' code.

Algebraic design of declarative systems gives a familiar tool for engineers who wish to design more managable systems in a functional
way. Object Oriented design patterns have also been useful in building declarative systems, but it is arguable whether the effort has
led to significant gains in managing the complexity of code. Humans naturally understand "what things do" rather than "what things are",
and it is debatable whether an engineer can build a clear design of "what things are" in the current state of the art, where unstructured
JSON is typical, and the Agile framework where goals take precidence over design is the current trend. Functional design patterns
are simply easier to understand. If engineers have regular code reviews, teams can easily reap rewards in the form of less, and more modular
code.
