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

source_url: https://github.com/microsoft/TypeScript-Website/blob/v2/packages/documentation/copy/en/get-started/TS%20for%20JS%20Programmers.md
revision: 62bc6ab326f2ac28f2202c39b2b75914cf0a2628
status: ready

title: TypeScript para pessoas programadoras JavaScript
short: TypeScript para pessoas programadoras JS
layout: docs
permalink: /docs/handbook/typescript-in-5-minutes.html
oneline: Aprenda como o TypeScript estende o JavaScript.
---

O TypeScript tem uma relação peculiar com o JavaScript.
O TypeScript oferece todos os recursos do JavaScript, além de uma camada
adicional: o sistema de tipos do TypeScript.

Por exemplo, o JavaScript fornece tipos primitivos como `string` e `number`, mas
não verifica se você os atribuiu de forma consistente.
O TypeScript verifica.

Isso significa que seu código JavaScript que funciona também é código
TypeScript.
O principal benefício do TypeScript é que ele pode destacar comportamentos
inesperados no seu código, reduzindo a probabilidade de erros.

Este tutorial oferece uma breve visão geral do TypeScript, com foco em seu
sistema de tipos.

## Tipos por inferência

O TypeScript conhece a linguagem JavaScript e, em muitos casos, gera tipos
automaticamente.
Por exemplo, ao criar uma variável e atribuir um valor específico a ela, o
TypeScript usará o valor como seu tipo.

```ts twoslash
let helloWorld = "Hello World";
//  ^?
```

Ao entender como o JavaScript funciona, o TypeScript consegue construir um
sistema de tipos que aceita código JavaScript, mas com tipos definidos.
Isso oferece um sistema de tipos sem a necessidade de adicionar caracteres
extras para explicitar os tipos no seu código.
É assim que o TypeScript sabe que `helloWorld` é uma `string` no exemplo acima.

Você pode ter escrito JavaScript no Visual Studio Code e usado o recurso de
autocompletar do editor.
O Visual Studio Code utiliza o TypeScript internamente para facilitar o trabalho
com JavaScript.

## Definindo tipos

Você pode usar uma grande variedade de padrões de projeto em JavaScript.
No entanto, alguns padrões de projeto dificultam a inferência automática de
tipos (por exemplo, padrões que usam programação dinâmica).
Para lidar com esses casos, o TypeScript oferece uma extensão da linguagem
JavaScript que permite especificar os tipos que devem ser usados.

Por exemplo, para criar um objeto com um tipo inferido que inclua `name: string`
e `id: number`, você pode escrever:

```ts twoslash
const user = {
  name: "Hayes",
  id: 0,
};
```

Você pode descrever explicitamente a forma deste objeto usando uma declaração de
`interface`:

```ts twoslash
interface User {
  name: string;
  id: number;
}
```

Em seguida, você pode declarar que um objeto JavaScript está em conformidade com
a estrutura da sua nova `interface` usando uma sintaxe como `: NomeDoTipo` após
a declaração de uma variável:

```ts twoslash
interface User {
  name: string;
  id: number;
}
// ---cut---
const user: User = {
  name: "Hayes",
  id: 0,
};
```

Se você fornecer um objeto que não corresponda à interface especificada, o
TypeScript exibirá um aviso:

```ts twoslash
// @errors: 2322
interface User {
  name: string;
  id: number;
}

const user: User = {
  username: "Hayes",
  id: 0,
};
```

Assim como o JavaScript suporta classes e programação orientada a objetos, o
TypeScript também suporta.
Você pode usar uma declaração de interface com classes:

```ts twoslash
interface User {
  name: string;
  id: number;
}

class UserAccount {
  name: string;
  id: number;

  constructor(name: string, id: number) {
    this.name = name;
    this.id = id;
  }
}

const user: User = new UserAccount("Murphy", 1);
```

Você pode usar interfaces para anotar parâmetros e valores de retorno de
funções:

```ts twoslash
// @noErrors
interface User {
  name: string;
  id: number;
}
// ---cut---
function deleteUser(user: User) {
  // ...
}

function getAdminUser(): User {
  //...
}
```

Já existe um pequeno conjunto de tipos primitivos disponíveis no JavaScript:
`boolean`, `bigint`, `null`, `number`, `string`, `symbol` e `undefined`, que
você pode usar em uma interface.
O TypeScript estende essa lista com alguns outros, como `any` (permite qualquer
coisa), [`unknown`](/play#example/unknown-and-never) (garante que quem usar esse
tipo declare qual é o tipo), [`never`](/play#example/unknown-and-never) (é
impossível que esse tipo ocorra) e `void` (uma função que retorna `undefined` ou
não tem valor de retorno).

Você verá que existem duas sintaxes para construir tipos:
[`interfaces` e `types`](/play/?e=83#example/types-vs-interfaces).
Você deve preferir `interface`.
Use `type` quando precisar de recursos específicos.

## Compondo tipos

Com TypeScript, você pode criar tipos complexos combinando tipos simples.
Existem duas maneiras populares de fazer isso: uniões e genéricos.

### Uniões

Com uma união, você pode declarar que um tipo pode ser um de vários tipos.
Por exemplo, você pode descrever um tipo `boolean` como sendo `true` ou `false`:

```ts twoslash
type MyBool = true | false;
```

_Nota:_ Se você passar o cursor sobre `MyBool` acima, verá que ele é
classificado como `boolean`.
Essa é uma propriedade do sistema de tipos estruturais.
Mais detalhes abaixo.

Um caso de uso popular para tipos de união é descrever o conjunto de
[literais](/docs/handbook/2/everyday-types.html#literal-types) de `string` ou
`number` que um valor pode assumir:

```ts twoslash
type WindowStates = "open" | "closed" | "minimized";
type LockStates = "locked" | "unlocked";
type PositiveOddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;
```

As uniões também oferecem uma maneira de lidar com tipos diferentes.
Por exemplo, você pode ter uma função que recebe um `array` ou uma `string`:

```ts twoslash
function getLength(obj: string | string[]) {
  return obj.length;
}
```

Para descobrir o tipo de uma variável, use `typeof`:

| Tipo      | Predicado                          |
| --------- | ---------------------------------- |
| string    | `typeof s === "string"`            |
| number    | `typeof n === "number"`            |
| boolean   | `typeof b === "boolean"`           |
| undefined | `typeof undefined === "undefined"` |
| function  | `typeof f === "function"`          |
| array     | `Array.isArray(a)`                 |

Por exemplo, você pode fazer com que uma função retorne valores diferentes
dependendo se ela recebe uma string ou um array:

<!-- prettier-ignore -->
```ts twoslash
function wrapInArray(obj: string | string[]) {
  if (typeof obj === "string") {
    return [obj];
//          ^?
  }
  return obj;
}
```

### Genéricos

Os genéricos fornecem variáveis ​​para tipos.
Um exemplo comum é um array.
Um array sem genéricos poderia conter qualquer coisa.
Um array com genéricos pode descrever os valores que o array contém.

```ts
type StringArray = Array<string>;
type NumberArray = Array<number>;
type ObjectWithNameArray = Array<{ name: string }>;
```

Você pode declarar seus próprios tipos que utilizam genéricos:

```ts twoslash
// @errors: 2345
interface Backpack<Type> {
  add: (obj: Type) => void;
  get: () => Type;
}

// Esta linha é um atalho para dizer ao TypeScript que existe uma constante
// chamada `backpack`, e para não se preocupar com a sua origem.
declare const backpack: Backpack<string>;

// object é uma string, porque o declaramos acima como parte da variável
// Backpack.
const object = backpack.get();

// Como a variável backpack é uma string, você não pode passar um número para a
// função add.
backpack.add(23);
```

## Sistema de tipos estruturais

Um dos princípios fundamentais do TypeScript é que a verificação de tipos se
concentra na _forma_ que os valores possuem.
Isso às vezes é chamado de "tipagem dinâmica" ou "tipagem estrutural".

Em um sistema de tipos estruturais, se dois objetos têm a mesma forma, eles são
considerados do mesmo tipo.

```ts twoslash
interface Point {
  x: number;
  y: number;
}

function logPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}

// loga "12, 26"
const point = { x: 12, y: 26 };
logPoint(point);
```

A variável `point` nunca é declarada como sendo do tipo `Point`.
No entanto, o TypeScript compara a forma de `point` com a forma de `Point` na
verificação de tipos.
Elas têm a mesma forma, então o código é aprovado.

A correspondência de forma exige apenas que um subconjunto dos campos do objeto
corresponda.

```ts twoslash
// @errors: 2345
interface Point {
  x: number;
  y: number;
}

function logPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}
// ---cut---
const point3 = { x: 12, y: 26, z: 89 };
logPoint(point3); // loga "12, 26"

const rect = { x: 33, y: 3, width: 30, height: 80 };
logPoint(rect); // loga "33, 3"

const color = { hex: "#187ABF" };
logPoint(color);
```

Não há diferença entre como classes e objetos obedecem a formas:

```ts twoslash
// @errors: 2345
interface Point {
  x: number;
  y: number;
}

function logPoint(p: Point) {
  console.log(`${p.x}, ${p.y}`);
}
// ---cut---
class VirtualPoint {
  x: number;
  y: number;

  constructor(x: number, y: number) {
    this.x = x;
    this.y = y;
  }
}

const newVPoint = new VirtualPoint(13, 56);
logPoint(newVPoint); // loga "13, 56"
```

Se o objeto ou classe tiver todas as propriedades necessárias, o TypeScript dirá
que elas correspondem, independentemente dos detalhes de implementação.

## Próximos passos

Esta foi uma breve visão geral da sintaxe e das ferramentas usadas no TypeScript
no dia a dia.
A partir daqui, você pode:

- Ler o manual completo [do início ao fim](/docs/handbook/intro.html)
- Explorar os [exemplos do Playground](/play#show-examples)
