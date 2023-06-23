# How to Create a Single File Bundle of a Large Typescript Project in 2023

I've been struggling with how to package a large 'monorepo' typescript project with several sub-projects inside an npm workspace.

Ideally I want a single file (two if you count the typedef file) to act as the distributable.

This is a _very_ simple ask, yet though many packaging tools semi-claim to do something like this, I've only found one that works reliably.

# How to build a 'single file' TypeScript/JavaScript Bundle

Use [esbuild](https://esbuild.github.io/) to compile entire TypeScript monorepo to a single large JavaScript file.

Create a file called `build.js`

```ts
const { build } = require("esbuild");
const { dependencies, peerDependencies } = require('./package.json');

const sharedConfig = {
  entryPoints: ["src/index.ts"],
  bundle: true,
  minify: false,
  // only needed if you have dependencies
  // external: Object.keys(dependencies).concat(Object.keys(peerDependencies)),
};

build({
  ...sharedConfig,
  platform: 'browser',
  format: 'esm',
  outfile: "dist/index.js",
});
```

And run it like: 
```sh
$ node ./build.js
```

Use [dts-bundle-generator](https://github.com/timocov/dts-bundle-generator) to build as single TypeScript defintion (.d.ts) file.

NOTE: this is a slow process on a large project, can take a few minutes.
```sh
$ npx dts-bundle-generator -o dist/index.d.ts src/index.ts
```

## What this accomplishes

- A _single_ javascript file with NO weird workspace-sub-project import dependencies (that tools like `npm pack` deal poorly with)
- A _single_ typescript definition file with NO weird workspace-sub-project import dependencies.

In a perfect world npm workspaces would just be recognized and dealt with properly. In my experience this simply isn't the case with `npm pack` which _unfortunately_ is the ONLY mechanism to create a _closed source_ 'real distributable' in the npm world.

