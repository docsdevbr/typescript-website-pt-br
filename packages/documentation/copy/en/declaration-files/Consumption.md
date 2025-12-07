---
# Copyright (c) Microsoft Corporation.
# Microsoft, Windows, Microsoft Azure and/or other Microsoft products and
# services referenced in the documentation may be either trademarks or
# registered trademarks of Microsoft in the United States and/or other
# countries.
# The licenses for this project do not grant you rights to use any Microsoft
# names, logos, or trademarks.
# Microsoft's general trademark guidelines can be found at
# https://go.microsoft.com/fwlink/?LinkID=254653.
#
# Documentation licensed under the Creative Commons Attribution 4.0
# International License.
# The original work was translated from English into Brazilian Portuguese.
# https://github.com/microsoft/TypeScript-Website/blob/-/LICENSE

title: Consumption
layout: docs
permalink: /docs/handbook/declaration-files/consumption.html
oneline: "How to download d.ts files for your project"
---

## Downloading

Getting type declarations requires no tools apart from npm.

As an example, getting the declarations for a library like lodash takes nothing more than the following command

```cmd
npm install --save-dev @types/lodash
```

It is worth noting that if the npm package already includes its declaration file as described in [Publishing](/docs/handbook/declaration-files/publishing.html), downloading the corresponding `@types` package is not needed.

## Consuming

From there you’ll be able to use lodash in your TypeScript code with no fuss.
This works for both modules and global code.

For example, once you’ve `npm install`-ed your type declarations, you can use imports and write

```ts
import * as _ from "lodash";
_.padStart("Hello TypeScript!", 20, " ");
```

or if you’re not using modules, you can just use the global variable `_`.

```ts
_.padStart("Hello TypeScript!", 20, " ");
```

## Searching

For the most part, type declaration packages should always have the same name as the package name on `npm`, but prefixed with `@types/`,
but if you need, you can use the [Yarn package search](https://yarnpkg.com/) to find the package for your favorite library.

> Note: if the declaration file you are searching for is not present, you can always contribute one back and help out the next developer looking for it.
> Please see the DefinitelyTyped [contribution guidelines page](https://definitelytyped.org/guides/contributing.html) for details.
