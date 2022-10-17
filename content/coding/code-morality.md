# When Things Go Wrong in Software

In software, as in life, things go 'wrong'.

In software, as in life, how one _reacts_ to bad situations is the only thing under our control.

How does one handle the 'bad things' in the domain of software? 

Below is a crystallization of [decades of software development experience](https://www.linkedin.com/in/matthewjosephtaylor) for how to deal with 'bad and unexpected things' in the realm of code.

I'll leave the life part for another article, but feel free to make analogies from what I write below. :) 


## Just Give Up

A common pattern is to simply _not_ deal with problems.

This is the ['Exception'](https://en.wikipedia.org/wiki/Exception_handling).

There are times when there is simply nothing that can be done, and the best one can do is fail as gracefully as possible.

This pattern works up to a point but is obviously not ideal. Think of it as the _default_ solution. What will happen if nothing is done. Leaving someone 'higher up' to deal with picking up the pieces.

## Leave No Room for Error

One can adopt [Functional Programming](https://en.wikipedia.org/wiki/Functional_programming) patterns.

The two main patterns one can adopt from FP are ['immutability'](https://en.wikipedia.org/wiki/Immutable_object), and writing ['side effect free'](https://en.wikipedia.org/wiki/Side_effect_(computer_science)) functions.

In a way these are both the same thing, one locks down _data_ and the other locks down _execution_. 

A handy way of thinking about this is that one _removes_ the _time_ component. Hence, one is protected from the future as long as 1+1=2 continues to hold, or more correctly, that one's concepts of these things hold (1+1 doesn't always equal 2 under all circumstances).

## Acknowledge Reality

There is a sort of middle-ground between giving up (Exceptions), and limiting oneself to computational domains that can't contain problems (pure FP).

One can produce results that aren't entirely _good_, and indeed have a _mix_ of _good_ and _bad_.

One can elevate the `Error` to a first class citizen.

This is quite helpful when dealing with the 'real world' where things are messy and bad things are _expected_ to happen from time to time.

What this means in practice is that instead of always returning a _valid_ result inside a function, one returns a combination of valid-or-errorful result.

TypeScript 'Errorful' result example:
```ts
function foo(input:string): string | Error {
  if(input.length > 8) {
    return new Error("Too many characters")
  }
  return `${input} was a triumph`

}
```

Note that one can also semi-achieve this with simple try-catch blocks, but this can get _really_ messy _really_ quick as the error processing becomes more complex.

I will argue that treating errors as _legitimate values_ gives one better tools for handling errors in many circumstances.

This is more than merely a style-preference. 

In languages such as TypeScript where the Exceptions are not part of the call-signature (as they are in say Java) this can allow one more visibility into what the errors _are likely to be_, and therefore have strategies for dealing with them (one can sub-class errors, and/or have a _generic_ error that can be parameterized).

## Summary

'Bad Things' happen.

There is no single 'best way' to deal with unexpected/bad situations, but one can _prepare_ and adopt better and better _strategies_ for handling those situations.

💩 happens, expecting the worst, and preparing for how to deal with it, often leads to better results. :)