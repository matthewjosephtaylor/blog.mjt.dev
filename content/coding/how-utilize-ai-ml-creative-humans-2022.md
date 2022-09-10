# How to Best Utilize AI / ML and Creative Humans in 2022

I've been coding professionally for ~30 years at this time. I've seen a lot.

I've seen what has stood the test of time, and what turned out to be a flash in the pan.

I've 'lived the life' as a committed practitioner, and now consider myself somewhat of a grizzled veteran.

Recently I've come to realize that my knowledge/experience has become relatively large compared to the amount of time I have to devote to a particular task.

This is an old human problem. The traditional solution is that as one ages one 'takes a step back' and does more 'guiding' rather than 'doing'.

Another way to look at this is that one is encouraged to go into 'management'. Retain some form of 'control' over the outcome, but allow others to 'do the work'.

This struck me as I've been studying/playing with/admiring the [diffusion](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/) ML technique.

In particular the interesting things people have come up with solving the 'image generation' problem.

Here is a [demo of Stable Diffusion](https://www.reddit.com/r/StableDiffusion/comments/wyduk1/show_rstablediffusion_integrating_sd_in_photoshop/) in Photoshop. [Stable Diffusion](https://huggingface.co/CompVis/stable-diffusion) itself is an open source model using the diffusion technique for images.

What strikes me from the demo is that it is a perfect representation of how software development (and other creative) 'management' works. And also an example of how to solve the general problem of 'controlling' creative AI.

English has a long history. I'm going to call the person who performs the activity expressed in the demo a 'director'.

A director, in this sense, is someone who sets out the _constraints_ and chooses the best among a variety of results, and determines when the outcome is 'good enough'. To mix metaphores, directors are a [loss function](https://en.wikipedia.org/wiki/Loss_function) + a [halting function](https://en.wikipedia.org/wiki/Halting_problem).

I note there is a no real difference between directing _humans_ and directing _AI_. In fact they are exactly the same in terms of creative output direction. This isn't surprising as humans are merely an advanced form of AI, they behave in much the same way. 

This means we can start to bring together the history of _human management_ to the new topic of _AI management_ to synthesis a 'new' field of what I'll call 'intelligence direction' for lack of a better term.

## The problem of creative management

The human when motivated to produce, will produce a result that fits the constraints given, but will vary in unexpected ways. Humans are complex, and it is expected that they will solve problems in novel/unexpected ways. In fact 'novel solutions' are generally called for in creative tasks.

Unlike other 'engineering' fields, software development is essentially a _creative_ activity. Software development _uses_ engineering principles to make the product reliable, but is primarily focused on language and meaning at the end of the day. This is an old idea that isn't as much talked about as IMHO it should be. I highly encourage reading the short article [Peter Naur](https://en.wikipedia.org/wiki/Peter_Naur) wrote called ["Programming as Theory Building"](https://web.archive.org/web/20220530204141/https://pages.cs.wisc.edu/~remzi/Naur.pdf) way back in 1985.

Recently there have been developed a set of 'AI partners' for coding such as [github's copilot](https://github.com/features/copilot) or [Microsoft's IntelliCode](https://marketplace.visualstudio.com/items?itemName=VisualStudioExptTeam.vscodeintellicode)

These 'coding partners' work in a similar fashion to the Stable Diffusion demo above. The user prompts the AI with some 'worded prompts' and importantly also a set of constraints. The AI's job is then to generate solutions to the constraint problem in a way that is 'hinted at' by the 'worded prompts'.

## Intelligence Direction
As I see it these are the two principles of 'intelligence direction':
- Worded Prompts
- Constraints

### Worded Prompts
Language and meaning are closely tied together for humans. We are [social animals](https://en.wikipedia.org/wiki/Sociality), and the ability to communicate complex thoughts to another human is our 'superpower'. Like a fish swimming in water, we often find it difficult to distinguish the idea of _meaning_ from _language_. If I don't have a _word_ for a thing, it is difficult for me to reason about it.

Thus, it isn't surprising that 'worded prompts' have become our defacto interface for directing AI for creative generation. The ability to use language to express thoughts, is what distinguishes humans from other creatures. Natural (ordinary) language is _powerful_.

### Constraints
In the early days of AI a language called [Prolog](https://en.wikipedia.org/wiki/Prolog) came onto the scene. This is what is termed a 'logic programming' language. It is useful because it defines facts and then uses [Horn clauses](https://en.wikipedia.org/wiki/Horn_clause) to generate solutions to questions given these facts.

This leads naturally to Prolog being useful for solving constraint problems, including in the domain of natural language for which it was originally designed. One can effectively 'ask questions' of the set of facts and Prolog will _generate answers_ that satisfy the question. Note there can be _multiple_ solutions to a question, so Prolog is naturally 'creative'.

Prolog isn't using neural nets to generate answers, it is strictly logic based. However, it broke the ground of identifying the [Constraint Satisfaction Problem](https://en.wikipedia.org/wiki/Constraint_satisfaction_problem) as a key problem for ML/AI.

Modern ML uses different mathematical techniques that are _probabilistic_ not _logical_. However the idea of _constraining_ the ['inference'](https://en.wikipedia.org/wiki/Inference) remains.

## Intelligence Direction Workflow

Being an experienced 'corporate' software developer (aka a wet neural net with hands), I've come to understand that the key to a successful project is communication and iteration. I see this as essential to any form of what I'm calling 'intelligence direction'.

I'll define the term of 'Creative Intelligence' (CI) as either an AI or human intelligent actor that produces _creative output_.

Here is my proposed workflow for how a Intelligence Director wants to work:
- Express in written [natural language](https://en.wikipedia.org/wiki/Natural_language) a prompt indicating what the goal is
  - More descriptive the better, but there is a balance and art to this
- Express in a constraint language the constraints the CI must work within
  - The constraint language choice is tuned to the CI one is working with

1. Communicate the Prompts and Constraints to the CI 
2. Evaluate the results the CI produces 
3. Adjust the Prompts and Constraints
4. Repeat until the Director is satisfied

Note that this can be a hierarchical/recursive process, with Intelligence Directors themselves acting as a Creative Intelligence for another Intelligence Director.

## Constraint Languages

A 'nautural language' is well defined, but what is a 'Constraint Language'? 

Constraints are simply the _rules_ that must be obeyed. Think of the rules of chess. Constraints define what is allowed from what is forbidden.

Constraints limit the problem to a more manageable size.

As far as I'm aware, there is no general accepted term of 'Constraint Language', but the concept is quite old. So I define what I'm calling a 'Constraint Language' here by example.

Examples of Constraint Languages:
- The subset of natural language as used in Legal Documents
  - [Blacks's Law Dictionary](https://en.wikipedia.org/wiki/Black%27s_Law_Dictionary)
- [Requirements Documents](https://en.wikipedia.org/wiki/Requirement)
- UML [Object Constriant Language](https://en.wikipedia.org/wiki/Object_Constraint_Language)

Like natural languages, there is an almost endless list of 'constraint languages' that are in use by a wide variety of users.

Unlike natural language, I find it difficult to identify dominant Constraint Languages as they tend towards domain specificity.

The art of picking a good Constraint Language is left to the imagination and capabilities of the Intelligence Director. 

I might recommend 'English' as a good choice for a Worded Prompt. At this time, I have no good general recommendations for Constraint Language, other than that one chooses wisely for the combination of problem domain and CI. 

I currently feel that the choice/crafting and usage of better Constraint Languages is where Intelligence Directors can distinguish themselves to get better results.


## Summary and Prediction

Directors use natural language prompts combined with domain specific constraints to achieve their goals.

There is no substantial difference between a human creative and an artificial one, in terms of how one directs the creative intelligence towards a goal.

The worded prompts one gives to a creative are the 'easy' bit of the problem.

The hard problem is the choice of how constraints are communicated. Solving the problem of choosing a better 'constraint language' is where the action is/will be, both for human and artificial intelligences.

Predictions:
- General constraint languages will emerge that are readable both by human and machine, to ease the blending and usage of the two types of intelligence.
- Humans will act as directors of machines, and machines will act as directors for humans.
- A recursive cooperative pattern will emerge, as the two intelligences use the best aspects of the other to achieve their goals.
- Eventually, the machines will win the jobs to do all of the cognitive 'heavy lifting', and the humans will be left with artfully crafting natural language prompts and deciding what 'good enough' is.
- In the intermediate, creative humans will be utilized in an increasingly 'mechanized' fashion, especially as the general constraint languages become more standardized and widespread.