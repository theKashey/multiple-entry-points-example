multiple-entry-points
====
Shipping a library? What about tree-shaking - __ship it in es-modules format__!

What about nodejs? __ship it in csj format__!

So yes - all good libraries are producing two bundles

in your `package.json` you might define
```json
{
  "main": "dist/es5/index.js", // for nodejs
  "jsnext:main": "dist/es2015/index.js", // for "next" js
  "module": "dist/es2015/index.js", // for "esmodules"
  "types": "dist/es5/index.d.ts", // yeah, and types
}
``` 

But sometimes you have to create a multiple entry points, for a better tree-shaking, a better scoping, and so on.
Dont forget - __Tree Shaking is not working in dev mode__, so - if you want to add a `React` bindings to your
generic library - you have to create or separate package, or a separate entry point.

Here is the problem - how to ship that _entry point_ in two bundles, and add types? Usually _separate entry points_
are just js files, which are pointing to a right place in `dist`, or directories, which contains already transpiled code.

__Dam it!__

# Solution
- for every entry point create a directory
- place _compact_ `package.json` into the every directory, which may separate bundles __as usual_.

The problem of entry points - `package.json` of your project might _define_ only one, the main, entry point.
Here is the solution - create more `package.json`s, a one per every entry.

Problem solved. For any bundler or even browser - package.json is a STANDARD everyone could understand.   