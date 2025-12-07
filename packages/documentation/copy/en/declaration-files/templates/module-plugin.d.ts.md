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

title: "Module: Plugin"
layout: docs
permalink: /docs/handbook/declaration-files/templates/module-plugin-d-ts.html
---

For example, when you want to work with JavaScript code which extends another library.

```ts
import { greeter } from "super-greeter";

// Normal Greeter API
greeter(2);
greeter("Hello world");

// Now we extend the object with a new function at runtime
import "hyper-super-greeter";
greeter.hyperGreet();
```

The definition for "super-greeter":

```ts
/*~ This example shows how to have multiple overloads for your function */
export interface GreeterFunction {
  (name: string): void
  (time: number): void
}

/*~ This example shows how to export a function specified by an interface */
export const greeter: GreeterFunction;
```

We can extend the existing module like the following:

```ts
// Type definitions for [~THE LIBRARY NAME~] [~OPTIONAL VERSION NUMBER~]
// Project: [~THE PROJECT NAME~]
// Definitions by: [~YOUR NAME~] <[~A URL FOR YOU~]>

/*~ This is the module plugin template file. You should rename it to index.d.ts
 *~ and place it in a folder with the same name as the module.
 *~ For example, if you were writing a file for "super-greeter", this
 *~ file should be 'super-greeter/index.d.ts'
 */

/*~ On this line, import the module which this module adds to */
import { greeter } from "super-greeter";

/*~ Here, declare the same module as the one you imported above
 *~ then we expand the existing declaration of the greeter function
 */
export module "super-greeter" {
  export interface GreeterFunction {
    /** Greets even better! */
    hyperGreet(): void;
  }
}
```

This uses [declaration merging](/docs/handbook/declaration-merging.html)

## The Impact of ES6 on Module Plugins

Some plugins add or modify top-level exports on existing modules.
While this is legal in CommonJS and other loaders, ES6 modules are considered immutable and this pattern will not be possible.
Because TypeScript is loader-agnostic, there is no compile-time enforcement of this policy, but developers intending to transition to an ES6 module loader should be aware of this.
