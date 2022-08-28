# How to TypeScript and NPM in 2022

After years of struggle I've finally found a way to get NPM and TypeScript to play nice together in a home-lab environment, and perhaps for the world in general.

In a nutshell the problem is incompatible module systems between nodejs and the browser, and the fact that NPM wants to be _javascript_ not _typescript_.

Turns out there is an easy solution for this I never ran across or thought about until today.

Here is the trick:

To `package.json` add:
```json
"scripts": {
    "postinstall": "tsc"
  }
```

This is effectively the same technique that is used to compile 'native binaries' for an npm package.

`postinstall` will _compile_ the typescript into javascript after the module is installed into `node_modules`

IMHO _every_ typescript project should be using this, and I'm surprised this isn't more widely used and standard. Perhaps it is, and I've simply missed it.

An example of this working can be found in my [Sqlites](https://github.com/matthewjosephtaylor/mjtdev-sqlites) project.

This finally unlocks the ability to use git as a npm 'install src' for me. That is HUGE for my workflow.

Yes I _could_ have compiled the typescript down to javascript and published that in my git repos as well, but I found it morally repugnant to include 'compiled source' in the project git source tree.

My old solution was using 'folder links' ala `npm instal ../../path-to-private-code`, which I'm happy to say is now obsolete.

I also get the benefit of _automatic version control_ of the source dependencies, as this will place the git commit inside the `package-lock.json` at the time of last `npm install`.

This means that I can happily hack on dependencies, without fear of breaking earlier projects that depended on the older code.

I work on a lot of projects, and have a great deal of 'personal library code' that I've accumulated, and continue to accumulate over time. I have my own private git+ssh service for private code (Raspberry Pi FTW), and then of course github for public code.

With this solution I can now happily take full advantage of git+npm while living the TypeScript dream. :)

