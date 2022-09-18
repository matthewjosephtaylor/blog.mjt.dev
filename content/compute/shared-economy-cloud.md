# The Shared Economy Cloud Infrastructure is a Thing

I'm reaching the point where I want to deploy and run my ML creations and experiments but don't want to pay an arm and a leg for hosting.

Instead of Google/AWS for GPU-heavy hosting I'm begining to be quite interested in an alternative.

[Vast.ai](https://vast.ai/) has been around for a few years. As far as I'm aware they are the 'market leader' in the segment of [sharing economy](https://en.wikipedia.org/wiki/Sharing_economy) focusing on ML workloads. I'm not affiliated, but I think they have a neat service.

It all comes down to giving up a bit of privacy and security for radically reduced costs.

This is exactly the same value proposition as Uber and Airbnb, only in  the computational domain.

## Costs

Nothing in life is free.

At the time of writing an [RTX 3090 TI costs $1100 on amazon](https://amzn.to/3LsdfWv)

Then the expense of the CPU/Memory/SSD/Motherboard/Power Supply/Case, etc.. Probably at least another $2K for anything remotely decent.

That is a $3K upfront cost. That takes a lot of GPU/hrs to justify.

Cost of renting an RTX 3090 on Vast.ai on Sept 18th 2022:
- On demand price $0.3/hr ~ $7.2/day ~ $216/mo ~ $2592/yr
- Interruptible price = $0.1/hr ~ $2.6/day ~ $77/mo ~ $924/yr

The trade off between security and cost extends to SLA as can be seen above.

Neither 'on demand' or 'interruptible' is going to give 100% uptime, but there are in theory more guarantees of uptime with 'on demand', so it costs 3x more (which is still quite cheap in comparison to AWS for similar hardware).


## Flexible Advantages

The neat thing is that one can be a customer and a supplier in this market.

The choice isn't buy vs rent, a new option of buy and rent-out is also on the table.

So perhaps spend $3k on a private ML rig and get the best of both worlds. :)

## Cheap ML for Startups and Small Business

As long as one can mitigate and/or accept the data privacy concerns, it feels to me that there is a real opportunity here. Especially for small 'Proof of Concept' / Startup projects.

I see no reason why one cant use this as a sort of [Heroku](https://www.heroku.com/) backend for GPU-heavy tasks.

## The Next Stage of Computing?

There is a constant tension between the one and the many.

In the computing realm this is seen as the fight between the 'personal computer' and the 'cloud'. It is an old, endless fight.

The field of 'shared computing' allows for a smoother balance in the tension, and the institution of the sharing economy has proved it is here to stay. 

IMHO shared compute is barely starting. But, it is hard to see how it won't become dominant given time. 

The economics are just too good, and at the end of the day: economics always wins.


## Serverless GPU?

Thanks to [cloudflare webworkers](https://workers.cloudflare.com/) and  [AWS Lambda](https://aws.amazon.com/lambda/) serverless computing is IMHO the only way to serve web-focused code in 2022.

Presently I'm not aware of anyone offering GPU resources on the level of the 'function call' aside from web APIs which is quite limiting.

I know I _personally_ would love such a service, and feel I'm not alone.

Not here yet, but hard to believe it won't be here soon.

# Blockchain Alternatives

It is 2022, everything is a blockchain right?

- [golem](https://www.golem.network/) is a blockchain-based CPU-only shared-compute system that [appears to have some traction](https://stats.golem.network/)
- [iExec](https://iex.ec/) is blockchain-based, and has GPU capabilities but [doesn't seem to have much traction yet](https://market.iex.ec/)

There are other projects that appear to be dead or haven't launched. I'd love to know of any active projects I missed.

Feels like the decentralized nature of the domain lends itself well to a decentralized payment system.

I'm honestly a bit surprised there are so few players in this space.

## Thought Experiments
Since I want it, but can't buy it yet, I am thinking to hack together my own private serverless GPU infrastructure using vast.ai and bubble gum. Maybe I'll throw in a pinch of blockchain just for spice. :)

I don't know if my playing around will ever become public/useful, but I'll update progress as I go along. If you have a similar idea hit me up. Perhaps we can share ideas. :)

It feels like this field of 'shared compute' is just getting started, and my mind is ablaze with projects I can use with it. Definitely vast.ai (and any competitors if I can find them) is going to get some time and a few of my moneys thrown at it/them.

There are too few hours in the day!

## Summary and Prediction

The sharing economy is not just for physical 'real world' rental.

One can use services like [Vast.ai](https://vast.ai/) or [Golem](https://www.golem.network/) today for ad-hoc computing at dramatically lower costs compared to traditional cloud providers.

Predictions:
- Easy 'Compute Sharing' apps users will install on their owned hardware will become a standard thing.
- Sharing Economy-style Serverless CPU/GPU will start to exist within the next 1-2 years, and grow to compete with today's giants within the decade.
- The big datacenters will continue to grow, but their growth will be checked by the vast sea of the 'shared computing infrastructure'. 
- The line between personal/public computing infrastructure will become increasingly blurred.




