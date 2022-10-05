# How to Test Software in 2022

Prompts and Constraints.

If you've read any of my recent articles] these terms are clear. They are how I'm [currently viewing the entire software world](https://mjtdev.medium.com/how-to-best-utilize-ai-ml-and-creative-humans-in-2022-f729a8bd0524), and indeed much of the world in general.

Prompt: A small natural language (English, etc..) set of text that hints at the desired outcome.

Constraint: A _domain specific_ set of rules that set boundaries around the problem.

It is important that constraints are _automatable_. They should be so easy to use, they are almost invisible. Like gravity. Always there to the point that the one creating a solution is focused on the _problem itself_ not on wrestling with the boundaries of the problem. Constraints are _accepted_ and _internalized_ by the problem-solver, and are helps to _narrow_ and _focus_ the problem domain.

Prompts _describe_ the problem and solution. It is important that they are _human readable_. There may be specialized wording ([jargon](https://en.wikipedia.org/wiki/Jargon)) used, but it should be kept to a minimum. If jargon is used, it should be used _consistently_ so as not to create confusion. The goal of a good prompt is clear, concise communication.

## What is a Test?

In the constext of software development tests take on several roles:

- Constraints as described above
- Confidence building (building trust in the solution)
- Domain knowledge (understanding the problem)

I'll argue that writing software without tests is _impossible_. I can say this as I have a broad view of what a 'test' is.

One can open up a text editor and type random characters, but this is unlikely to yield a good result. 

The first 'test' one often encounters is the compiler/evaluator of the program. It will simply not do anything remotely useful unless it is satisfied.

From there one goes on to more and more sophisticated testing. Anything from type systems to linters to unit/integration/functional tests, etc...

Importantly, tests are _composable_. That is to say they are independent, and one can add and mix and match them without limit. One can always add a new test on the existing pile.

## Trust

Note that I added 'confidence building' as a key aspect of a test. As one deals with creating software, one realizes at the core, that one is dealing with _managing complexity over time_.

It is one thing to say one has a solution to a problem that worked once, it is another to say that one has a _reliable solution_ to a problem that is likely to work _over time_.

As one builds up a testing environment, one also builds in _trust_ that the written software does what is intended, and can that it be extended without fear. 

A good testing environment becomes _critically important_ as the project size grows. Eventually it becomes _impossible_ to add additional complexity (code) to a system unless one has trust in one's tests. [Regressions](https://en.wikipedia.org/wiki/Software_regression) will come to dominate otherwise.

In particular these tests MUST be automated so that they become _constraints_ to the project as a whole. This is what gives one the ability to solve _new_ problems (add features) within the context of an existing project's 'software ecosystem'.

## Tools/Frameworks/Paradigms

Over time _many_ testing tools and frameworks and paradigms have been developed.

There is no one 'right' tool/framework/paradigm for testing, and _there doesn't need to be_.

Testing is _composable_. This means one has the freedom to pick and choose, add and remove, as needs dictate.

It is _important_ to be smart and pick _good testing tools/frameworks/paradigms_, as this in many ways will determine the outcome one gets.

Software _moves fast_. It is important to ride the current waves, while also paying attention to overall larger trends.

Adopt and try out a bit of everything and see what eventually works. Don't be afraid to try new things, but also lean on experience to know what has proved useful in the past.

## Bureaucracy

I want to make a special note that 'too much of a good thing' is real.

It is _seductively easy_ to fall into the trap of a testing environment becoming _poisonous_ to the very project it is trying to serve.

As the testing environment becomes heavier and heavier, with more and more tests added to the mix, there is a _real danger_ that the testing environment becomes too overbearing. Progress itself becomes impossible, and the project _hardens_, even _fossilizes_, to the point that it can no longer _adapt quickly_, eventually it can no longer adapt at all.

Like most things in life, it is a balance. One is fighting _complexity_ and there are dangers on both the 'too much' and 'too little' side of the question of 'how much order to the chaos do I bring?'.

Bravery is the only solution to this I am aware of. One has to _tear down_ the very foundations of the _world_ to make it _better_. I'll note that for _good reasons_, this is a dangerous activity more likely to bring ruin than delight.

IMHO it is better to fight this fight in small chunks vs all at once. Recognize it is a _hard problem_ and _continual struggle_.

In other words, it is better to always be on continual guard for this problem, and be quick to tear down impediments to progress as they become recognized, _before_ aggressive 'revolutionary' solutions are needed which are a roll of the dice, more likely to kill the project than save it. 

## Tests as a Repository of Domain Knowledge

This is more of an 'advanced' use of testing environments. One I feel is often overlooked, especially on smaller projects.

The reality of software development is that individuals with _come and go_ as the project _continues_. 

The project _itself_ is its own entity. In business we have come to understand there is such a thing as a ['corporate person'](https://en.wikipedia.org/wiki/Corporate_personhood)

Unlike a 'coproarate person' a project doesn't have _legal rights_ (at least not as of the time of writing :) ) but I feel it is the correct lens from which to view any sufficiently large project.

After a while a successful project really does 'take on a life of its own', and I mean this in a non-derogatory, non-ironic way.

Tests _can_ be used to _store knowledge_ about the ['business domain'](https://en.wikipedia.org/wiki/Business_domain) that is stable and lasts over time.

One paradigm that attempts to incorporate this view is [Behavior Driven Development (BDD)](https://en.wikipedia.org/wiki/Behavior-driven_development). I'm not sure I'd recommend this particular approach/paradigm on the whole, but I do think one can use it 'lightly' and steal from it the 'good parts'.

In particular I think that BDD leads one to writing tests that expose the 'prompts' in clear, understandable natural language, that govern the project, paired with a 'constraint' that can be used as an automated test.

As new people are brought into the project, there is a natural place for them to go to _understand_ the project quickly. For instance, jargon and business rules can be defined 'by example' for those who can read code.

BDD falls into ['Test Driven Development' TDD](https://en.wikipedia.org/wiki/Test-driven_development). I think one can become 'too religious' on this topic and can lead to the nightmares of bureaucracy I described above. 

However, I do think the concept of pairing the natural language prompts with the code (constrint) in a way that both can be 'linked' together has great value (if it can be achieved) to strengthen the 'bones' of the project, and insure it stands the test of time.


## Summary

Testing is a critical area of software development. One is going to create a 'testing environment' whether one realizes it or not.

It is better to be conscious and deliberate (awake) when making the choices of a testing environment, as this environment can determine the fate of the project (whether one is aware of it or not).

There are no silver bullets. It will take time and effort. 

Prompts and Constraints are a good lens from which to view the problem of testing. Write clear, simple natural language for describing the 'business' side. Use fast, simple, effective testing tools/frameworks to constrain and therefore aid development. Use both prompts and constraints _linked together_ to gain confidence in the project, and ensure it has a long life.

