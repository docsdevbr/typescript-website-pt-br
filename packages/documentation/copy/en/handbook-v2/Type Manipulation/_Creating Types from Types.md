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

title: Creating Types from Types
layout: docs
permalink: /docs/handbook/2/types-from-types.html
oneline: "An overview of the ways in which you can create more types from existing types."
---

TypeScript's type system is very powerful because it allows expressing types _in terms of other types_.

The simplest form of this idea is generics. Additionally, we have a wide variety of _type operators_ available to use.
It's also possible to express types in terms of _values_ that we already have.

By combining various type operators, we can express complex operations and values in a succinct, maintainable way.
In this section we'll cover ways to express a new type in terms of an existing type or value.

- [Generics](/docs/handbook/2/generics.html) - Types which take parameters
- [Keyof Type Operator](/docs/handbook/2/keyof-types.html) - Using the `keyof` operator to create new types
- [Typeof Type Operator](/docs/handbook/2/typeof-types.html) - Using the `typeof` operator to create new types
- [Indexed Access Types](/docs/handbook/2/indexed-access-types.html) - Using `Type['a']` syntax to access a subset of a type
- [Conditional Types](/docs/handbook/2/conditional-types.html) - Types which act like if statements in the type system
- [Mapped Types](/docs/handbook/2/mapped-types.html) - Creating types by mapping each property in an existing type
- [Template Literal Types](/docs/handbook/2/template-literal-types.html) - Mapped types which change properties via template literal strings
