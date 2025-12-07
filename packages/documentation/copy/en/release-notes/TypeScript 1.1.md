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

title: TypeScript 1.1
layout: docs
permalink: /docs/handbook/release-notes/typescript-1-1.html
oneline: TypeScript 1.1 Release Notes
---

## Performance Improvements

The 1.1 compiler is typically around 4x faster than any previous release. See [this blog post for some impressive charts.](https://web.archive.org/web/20141007020020/http://blogs.msdn.com/b/typescript/archive/2014/10/06/announcing-typescript-1-1-ctp.aspx)

## Better Module Visibility Rules

TypeScript now only strictly enforces the visibility of types in modules if the [`declaration`](/tsconfig#declaration) flag is provided. This is very useful for Angular scenarios, for example:

```ts
module MyControllers {
  interface ZooScope extends ng.IScope {
    animals: Animal[];
  }
  export class ZooController {
    // Used to be an error (cannot expose ZooScope), but now is only
    // an error when trying to generate .d.ts files
    constructor(public $scope: ZooScope) {}
    /* more code */
  }
}
```
