# How to use Node.js `exports` with TypeScript

This repository has an example of how to use Node.js `exports` field in your `package.json` so that it works correctly with TypeScript.

This can be challenging, as TypeScript has multiple [module resolution strategies](https://www.typescriptlang.org/docs/handbook/module-resolution.html#module-resolution-strategies). 

This example works with `Node` (the default), and `Node16`, which support all the current Node.js module resolution rules.

This was tested with Node 16, but should work with any version starting at v12.7.0.

This was also tested with `"type": "module"` and it works correctly.

## Running the example

This example has its `node_modules` committed, so all you need to run it is cloning the repository and run `bash test.sh`.

## package.json description

The `package.json` that has the required settings for this to work is in `node_modules/dep/pacakge.json`. Here's an explanation of it:

* `main`: Not needed. Can be omitted.
* `types`: Used by TypeScript's `Node` resolution to resolve a bare import of the dependency (e.g. `import {a} from "dep";`).
* `exports`: Used by Node to resolve `require`/`import`s at runtime, and TypeScript's `Node16` resolution.
  * `"."`: Used to resolve a bare import of the dependency.
  * `"./other"`: Used to resolve a subpath import.
* `typesVersions`: Used by TypeScript's `Node` resolution to resolve subpath imports.

## Requirements

1. Every exported `.js` file should have its `.d.ts` file in the same folder, as the `Node16` resolution will resolve them based on the path that's decleared in `exports`.
