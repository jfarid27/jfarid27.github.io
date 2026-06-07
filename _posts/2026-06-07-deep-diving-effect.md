---
layout : post 
title  : My initial thoughts after a few months of Professional Effect 
snip   : Effect for the Brave and True 
---

A few months ago, I started to research more into [Effect](https://effect.website/) after
binge watching far too many videos on it. When I first saw it and mocked up some code
with it, my initial reaction was: "This is ok."

Some of the main selling points I have noticed are some clear advantages over
vanilla Typescript (yes, you read correctly. We are so old Typescript has a
vanilla version.)

1. Lifting Dependencies into the Type System.
2. Thunking all Effects so you have full runtime control over execution.
3. An emphasis on Monadic style "declarative" syntax, focusing on yields and Functional patterns like
map, flatMap, pipes, chains, etc.

There are a few more details but these are the highlights most developers talk about as converts to
the library.

At first, I mostly worked on small scripts and mock code to get used to the system. One of the first
things programmers start getting used to is generators, services, and error tagging.

```typescript
import { Effect, Data, Context } from "effect";

// Define a tagged error that the code will throw on failure.
class APIException extends Data.TaggedError("APIException") {}

// Define an interface for our service.
interface API {
    getUser(id: string): Effect.Effect<User, APIException>
}

// Define a tag for our service.
class APIService extends Context.Tag("APIService")<APIService, API>() {}

// Define a function that uses our service.
const useUser = (id: string): Effect.Effect<User, APIException> =>
  Effect.gen(function* () {
    const api = yield* APIService;
    return yield* api.getUser(id);
  });
  
// Create a program that can be imported by a consumer to fetch a user.
const useUserProgram = (id: string) => Effect.provideService(program, APIService, {
    getUser: (id: string) =>
        Effect.gen(function* () {
            // Actually fetch from the API.
            const result = yield* Effect.tryPromise(() => {
                try: () => fetch(`(...)/users/${id}`),
                catch: (error) => new APIException({ message: "Failed to fetch user." })
            });
            
            // Try to parse the JSON.
            const user = yield* Effect.tryPromise(() => {
                try: () => result.json(),
                catch: (error) => new APIException({ message: "Failed to parse user." })
            });
            return user;
        });
})
```

This is a simple program, right? It makes a decent call, now has a type of Effect<unknown, APIException, never> (success value, errors, and dependencies), and can run?

Wrong. I've gotten good at writing effect with the help of AI and IDEs, but it's not actually
finished. And yes, this chunk of code is huge. On top of this, I haven't even written an adapter
that mocks data for it to be used in a testing environment where you don't have access to a server.

_The user type is still unknown. You have to use Effect.Schema, lift it's expected shape into Effect,
and decode it._

_That parsing might also fail, throwing a ParseError you need to handle._

_There may be cases where a consumer, like a react component, may want to fallback to a default value._

_We haven't even gotten to the Jotai-style implementation of effect-atom._

While I said a few months ago I was testing out Effect, now that I'm using it professionally,
I'm somewhat concerned. When you're now forced to write code that complains when you don't handle
an error, or when you must provide implementations of dependencies, you have now looked under the bed
and saw just how many monsters there are when making anything using Javascript.

I have some funny thoughts on this particular realization:
1. Old hat developers were right to distrust the JS ecosystem. There are more ways for your programs to
fail and to fully encapsulate all its failures, requires a lot of code.
2. Old hat developers were also wrong. The reality is most Java developers exist in a world where most
don't have to deal with modern code and starting from scratch. It's easy to write safe code, when you're
inheriting an existing codebase and framework. Starting an entirely new product from scratch means you
have to make all the decisions about edge cases, parsings, default values, and error conditions.
3. AI doesn't really help. Effect is really only around 2 years old, and not many people are using it,
which means inference doesn't really have a great deal of training data on Effect patterns yet.
4. Is this Haskell at this point? Haskell developers have always been known for never getting anything done,
because all their programs simply take forever to write and cover all possible conditions.
5. This isn't a knock against Effect, but rather a realization that pure Javascript is generally bad,
[software still sucks](https://www.stilldrinking.org/programming-sucks), and most of the programs
written in the ecosystem are guaranteed to fail in production, since no one is writing systems with
this level of verbosity to ensure the code is actually robust. This is why software is breaking all
the time.

While I'm excited that more people are talking about developing with Effect in mind, I'm also concerned
that the language is just evolving to Java. At that point, why didn't we just include a JVM in every
browser and write that? There's plenty to say about why [Java was not chosen as the language of the
web](https://auth0.com/blog/a-brief-history-of-javascript/#The-Birth-of-JavaScript), but if you
told me the language would evolve to be a strongly typed language with more functional features,
I probably would have said, why not just use a language that already existed?

Seeing Javascript evolve from browser, to Node, to Typescript, and now to Effect makes me believe
Javascript really was meant to be a chameleon of the times. It is flexible enough to strap onto
the whatever the environment needs at the time, but because of that, is now arguably 4 different
languages, with 3 current competing JS runtimes (bun, node, and possibly deno), multiple package
registries (npm, jsr), extremely different viewpoints on front-end frameworks and a host of challenges just to get an app started and deployed.

At this point, I'm not really sure what Javascript actually is today, nor will I have any idea
what it will be in another 10 years. Where most developers expect restaurants with a menu, Javascript
is a buffet. You don't know what you're going to get, there's no set menu, and no one knows what
will be served in an hour, tomorrow, or next week.
