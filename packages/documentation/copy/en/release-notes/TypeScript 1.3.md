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

title: TypeScript 1.3
layout: docs
permalink: /docs/handbook/release-notes/typescript-1-3.html
oneline: TypeScript 1.3 Release Notes
---

## Protected

The new `protected` modifier in classes works like it does in familiar languages like C++, C#, and Java. A `protected` member of a class is visible only inside subclasses of the class in which it is declared:

```ts
class Thing {
  protected doSomething() {
    /* ... */
  }
}

class MyThing extends Thing {
  public myMethod() {
    // OK, can access protected member from subclass
    this.doSomething();
  }
}
var t = new MyThing();
t.doSomething(); // Error, cannot call protected member from outside class
```

## Tuple types

Tuple types express an array where the type of certain elements is known, but need not be the same. For example, you may want to represent an array with a `string` at position 0 and a `number` at position 1:

```ts
// Declare a tuple type
var x: [string, number];
// Initialize it
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"]; // Error
```

When accessing an element with a known index, the correct type is retrieved:

```ts
console.log(x[0].substr(1)); // OK
console.log(x[1].substr(1)); // Error, 'number' does not have 'substr'
```

Note that in TypeScript 1.4, when accessing an element outside the set of known indices, a union type is used instead:

```ts
x[3] = "world"; // OK
console.log(x[5].toString()); // OK, 'string' and 'number' both have toString
x[6] = true; // Error, boolean isn't number or string
```
