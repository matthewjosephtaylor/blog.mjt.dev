# AHA! Constrained Creative Intelligence Works Best

In a [previous article](../../content/coding/how-utilize-ai-ml-creative-humans-2022.md) I introduced a concept of a Creative Intelligence (CI) as either a human or AI that produces creative output. 

I introduced the term Intelligence Director (ID) as the one who directs the CI towards a goal.
I introduced the concept of a Constraint Language (CL) as a language used for _constraining_ the CI working on a given task.

This article builds on the previous, and focuses more on constraints and why they are so important for creativity.

## Less freedom = Better Creative Expression?

It is well known that constraints and art go hand in hand. Artists of all forms adopt self-imposed limitations to better express themselves.

At first glance this seems counter-intuitive. However, it makes sense once one thinks about it for a bit.

The blank canvas is the the most terrifying starting point for any creative endeavour, for good reason.

The example of [Buridan's ass](https://en.wikipedia.org/wiki/Buridan%27s_ass) gives good insight into one reason why this is so.

The more freedom one has, the more _choices_ one is forced to make. This leads to 'analysis paralysis'. 

By _constraining_ the 'canvas size', one has fewer choices to make. Fewer choices leads to a better quality, and a _more expected_ result. 
- Better, quality as one can devote more 'cycles' to each of the available choices. 
- More expected result, as there is _less room_ for 'error'.

## Both Human and Machine Intelligences Desire Constraint

As a software developer, one of the things I often deal with is something called a 'Requirements Document'.

This is a form of a constraint language for constraining software developers.

This document, however, is far from the total constraint set I usually develop under.

There are also:
- [Types](https://en.wikipedia.org/wiki/Type_system)
- [Linters](https://en.wikipedia.org/wiki/Lint_(software))
- [Unit Tests](https://en.wikipedia.org/wiki/Unit_testing)

Note that the above all automateable which has a host of benefits:
- Faster (near instant in many cases) feedback
- Clearer understanding, as there is less room for ambiguity

The more automatable the constraint language becomes, the more it comes to resemble a [loss function](https://en.wikipedia.org/wiki/Loss_function)

## Constraints First

The importance of constraints leads to an 'aha', about how better to direct both humans and machines going forward.

The key to starting a creative task is: 
- At the start, write the boundaries of the task in an unambiguous constraint language.

I don't claim this is a new idea. Perhaps it is a way of looking at the problem in a new light. A way to _generally_ focus and organize a creative task in an age where 'creativity' is being re-imagined, and is more 'commoditized' thanks to advances in ML.

I'm also not saying that these constraints won't be changed later. Constraints almost certainly will change, as the creative intelligence iterates over what it produces, and the director itself learns from the creative output. So choosing a constraint language one is/can become _fluent_ in, is likewise important.

I would recommend that the constraint language should be translatable to a set of tests, that each return a simple boolean passed/failed. In other words the constraint language should be _machine readable_.

Note that one is free to use all the available tools from Type Systems to Linters to Unit Tests to any sort of evaluation of what is creatively produced. I'm taking a broad view, and so my idea of a 'constraint language' could be thought of being composed by multiple 'languages' each with their own particular syntax and rules.

I don't think a _single_ constraint language is possible, as constraint languages are likely to be _domain specific_. Type Systems work wonderfully for code, but perhaps aren't well suited for Opera. It is hard to imagine a language syntax wide and expressive enough to cover everything. Happy to be proven wrong. :)

To be clear, the 'creative product' could be anything from a screenplay, to code, to music, to a static or moving image. Today the current 'hotness' is more about static image generation, but there are no practical limits that I can see. All creative expressiveness that is digitize-able is up for grabs.

Note that we are already doing this. The idea of using constraint languages is far from new. We pick TypeScript over Javascript because it gives better 'safety'. We choose to use a unit testing framework, and write a series of tests that must pass for better 'quality'. We use linters and git pre-commit rules, etc...

For me this is more of a mindset shift. It is an understanding that in order to get the _best_ out of a creative intelligence one must constrain it as much as is practical. We are already well underway for doing this in the field of computer science. Now it is the time for the other artistic domains to follow suit.


## Summary and Prediction

The 'constraints first' approach means that, at the first start, one must introduce as many constraints as are feasible, and focus on continually improving those constraints. 

One must understand that the _constraints_ are a critical part of efficiently finding a solution, not the creative intelligence, whose job is 'merely' to _produce_ results.

As time goes on, _machines_ will be the one doing more and more of the heavy lifting, and generating creative output. Today, generating creative output is relatively expensive, because humans are used for generation. Tomorrow, creative generation will become the domain of the machine. It will be the human's job to create prompts for the machine, and to constrain and judge creative output.

This means that effective tools for _constraining_ the creative output, will become more and more important for 'human productivity' as time goes on.

Predictions:
- A flourishing of new machine-readable constraint languages tailored for each creative domain.
- Human 'creativity' will become more about being fluent in domain specific constraint languages vs 'doing the work'.
- There will be much wailing and gnashing of teeth as humans loose 'creativity jobs' to machines.
- A new 'golden age' of creativity will emerge as everyone becomes a Picasso, and Picasso becomes Picasso².


