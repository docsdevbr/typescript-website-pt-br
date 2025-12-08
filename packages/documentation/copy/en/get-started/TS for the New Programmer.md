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

source_url: https://github.com/microsoft/TypeScript-Website/blob/v2/packages/documentation/copy/en/get-started/TS%20for%20the%20New%20Programmer.md
revision: 838cacec4a6f0cf032b487f583dffeeb70c46b8a
status: ready

title: TypeScript para a nova pessoa programadora
short: TS para a nova pessoa programadora
layout: docs
permalink: /docs/handbook/typescript-from-scratch.html
oneline: Aprenda TypeScript do zero
---

Parabéns por escolher TypeScript como uma de suas primeiras linguagens — você já
está tomando uma ótima decisão!

Você provavelmente já ouviu falar que TypeScript é uma "variante" ou "tipo" de
JavaScript.
A relação entre TypeScript (TS) e JavaScript (JS) é bastante singular entre as
linguagens de programação modernas, então aprender mais sobre essa relação
ajudará você a entender como o TypeScript agrega valor ao JavaScript.

## O que é JavaScript? Uma breve história

O JavaScript (também conhecido como ECMAScript) começou como uma linguagem de
script simples para navegadores.
Na época de sua criação, esperava-se que fosse usado para pequenos trechos de
código incorporados em uma página web — escrever mais do que algumas dezenas de
linhas de código seria algo incomum.
Por isso, os primeiros navegadores web executavam esse tipo de código muito
lentamente.
Com o tempo, porém, o JS se tornou cada vez mais popular e as pessoas
desenvolvedoras web começaram a usá-lo para criar experiências interativas.

As pessoas desenvolvedoras de navegadores responderam a esse aumento no uso do
JS otimizando seus mecanismos de execução (compilação dinâmica) e ampliando o
que podia ser feito com ele (adicionando APIs), o que, por sua vez, fez com que
as pessoas desenvolvedoras web o utilizassem ainda mais.
Em sites modernos, seu navegador frequentemente executa aplicações que abrangem
centenas de milhares de linhas de código.
Este é o crescimento longo e gradual da "web", começando como uma simples rede
de páginas estáticas e evoluindo para uma plataforma para _aplicações_ ricas de
todos os tipos.

Mais que isso, o JS se tornou popular o suficiente para ser usado fora do
contexto dos navegadores, como na implementação de servidores JS usando o
Node.js.
A natureza "executável em qualquer lugar" do JS o torna uma escolha atraente
para o desenvolvimento multiplataforma.
Há muitas pessoas desenvolvedoras hoje em dia que usam _apenas_ JavaScript para
programar toda a sua pilha de tecnologia!

Resumindo, temos uma linguagem que foi projetada para usos rápidos e que se
tornou uma ferramenta completa para escrever aplicações com milhões de linhas de
código.
Cada linguagem tem suas _peculiaridades_ — excentricidades e surpresas, e o
humilde início do JavaScript faz com que ele tenha _muitas_ delas.
Alguns exemplos:

- O operador de igualdade do JavaScript (`==`) _força_ seus operandos, levando a
  comportamentos inesperados:

  ```js
  if ("" == 0) {
    // É! Mas por quê??
  }
  if (1 < x < 3) {
    // Verdadeiro para *qualquer* valor de x!
  }
  ```

- O JavaScript também permite acessar propriedades que não estão presentes:

  ```js
  const obj = { width: 10, height: 15 };
  // Por que isso é NaN? Soletrar isso é difícil!
  const area = obj.width * obj.heigth;
  ```

A maioria das linguagens de programação lançaria um erro quando esse tipo de
erro ocorresse; algumas o fariam durante a compilação — antes mesmo da execução
do código.
Ao escrever pequenos programas, essas peculiaridades são irritantes, mas
gerenciáveis; ao escrever aplicações com centenas ou milhares de linhas de
código, essas surpresas constantes representam um problema sério.

## TypeScript: um verificador de tipos estático

Mencionamos anteriormente que algumas linguagens não permitem que programas com
erros sejam executados.
Detectar erros no código sem executá-lo é chamado de _verificação estática_.
Determinar o que é um erro e o que não é, com base nos tipos de valores com os
quais se está operando, é conhecido como verificação estática de _tipo_.

O TypeScript verifica um programa em busca de erros antes da execução, e faz
isso com base nos _tipos de valores_, tornando-o um _verificador de tipos
estático_.
Por exemplo, o último exemplo acima contém um erro devido ao _tipo_ de `obj`.
Aqui está o erro encontrado pelo TypeScript:

```ts twoslash
// @errors: 2551
const obj = { width: 10, height: 15 };
const area = obj.width * obj.heigth;
```

### Um superconjunto tipado de JavaScript

Mas como o TypeScript se relaciona com o JavaScript?

#### Sintaxe

O TypeScript é uma linguagem que é um _superconjunto_ do JavaScript: a sintaxe
do JS é, portanto, válida para TS.
Sintaxe se refere à maneira como escrevemos texto para formar um programa.
Por exemplo, este código tem um erro de _sintaxe_ porque está faltando um `)`:

```ts twoslash
// @errors: 1005
let a = (4
```

O TypeScript não considera nenhum código JavaScript como um erro devido à sua
sintaxe.
Isso significa que você pode pegar qualquer código JavaScript funcional e
colocá-lo em um arquivo TypeScript sem se preocupar exatamente com a forma como
ele está escrito.

#### Tipos

No entanto, o TypeScript é um superconjunto _tipado_, o que significa que ele
adiciona regras sobre como diferentes tipos de valores podem ser usados.
O erro anterior sobre `obj.height` não era um erro de _sintaxe_: é um erro de
uso incorreto de algum tipo de valor (um _tipo_).

Como outro exemplo, este é um código JavaScript que você pode executar no seu
navegador e ele _irá_ imprimir o log de um valor:

```js
console.log(4 / []);
```

Esse programa sintaticamente válido imprime o log `Infinity`.
O TypeScript, no entanto, considera a divisão de um número por um array uma
operação sem sentido e emitirá um erro:

```ts twoslash
// @errors: 2363
console.log(4 / []);
```

É possível que você realmente _tivesse_ a intenção de dividir um número por um
array, talvez apenas para ver o que aconteceria, mas na maioria das vezes, isso
é um erro de programação.
O verificador de tipos do TypeScript foi projetado para permitir a execução de
programas corretos, ao mesmo tempo que detecta o máximo possível de erros
comuns.
(Mais adiante, aprenderemos sobre as configurações que você pode usar para
definir o rigor com que o TypeScript verifica seu código.)

Se você mover algum código de um arquivo JavaScript para um arquivo TypeScript,
poderá ver _erros de tipo_, dependendo de como o código foi escrito.
Esses podem ser problemas legítimos com o código ou o TypeScript sendo
excessivamente conservador.
Ao longo deste guia, demonstraremos como adicionar várias sintaxes do TypeScript
para eliminar tais erros.

#### Comportamento em tempo de execução

O TypeScript também é uma linguagem de programação que preserva o _comportamento
em tempo de execução_ do JavaScript.
Por exemplo, dividir por zero em JavaScript produz `Infinity` em vez de lançar
uma exceção em tempo de execução.
Como princípio, o TypeScript **nunca** altera o comportamento em tempo de
execução do código JavaScript.

Isso significa que, se você migrar código de JavaScript para TypeScript, ele
**garante** que será executado da mesma forma, mesmo que o TypeScript considere
que o código contém erros de tipo.

Manter o mesmo comportamento em tempo de execução do JavaScript é uma promessa
fundamental do TypeScript, pois significa que você pode facilmente transitar
entre as duas linguagens sem se preocupar com diferenças sutis que possam fazer
seu programa parar de funcionar.

<!--
Subseção ausente sobre o fato de que o TS estende o JS para adicionar sintaxe
para especificação de tipo.
(Já que o texto imediatamente anterior estava entusiasmado com como o código JS
pode ser usado em TS.)
-->

#### Tipos apagados


Em linhas gerais, depois que o compilador do TypeScript termina de verificar seu
código, ele _apaga_ os tipos para produzir o código "compilado" resultante.
Isso significa que, após a compilação, o código JavaScript puro resultante não
contém informações de tipo.

Isso também significa que o TypeScript nunca altera o _comportamento_ do seu
programa com base nos tipos inferidos.
Em resumo, embora você possa encontrar erros de tipo durante a compilação, o
sistema de tipos em si não influencia o funcionamento do seu programa em
execução.

Por fim, o TypeScript não fornece nenhuma biblioteca de tempo de execução
adicional.
Seus programas usarão a mesma biblioteca padrão (ou bibliotecas externas) que os
programas JavaScript, portanto, não há nenhum framework específico do TypeScript
para aprender.

<!--
Este parágrafo deve ser expandido para mencionar que há uma exceção: permitir o
uso de recursos mais recentes do JavaScript e transpilar o código para uma
versão mais antiga, o que pode adicionar pequenos trechos de funcionalidade
quando necessário.
(Talvez com um exemplo --- algo como `?.` seria bom para mostrar às pessoas
leitoras que este documento está sendo mantido.)
-->

## Aprendendo JavaScript e TypeScript

Frequentemente vemos a pergunta "Devo aprender JavaScript ou TypeScript?".

A resposta é que você não pode aprender TypeScript sem aprender JavaScript!
O TypeScript compartilha sintaxe e comportamento de tempo de execução com o
JavaScript, então tudo o que você aprende sobre JavaScript está te ajudando a
aprender TypeScript ao mesmo tempo.

Existem muitos recursos disponíveis para pessoas programadoras aprenderem
JavaScript; você _não_ deve ignorar esses recursos se estiver escrevendo em
TypeScript.
Por exemplo, existem cerca de 20 vezes mais perguntas no StackOverflow com a tag
`javascript` do que com a tag `typescript`, mas _todas_ as perguntas com a tag
`javascript` também se aplicam ao TypeScript.

Se você se encontrar procurando por algo como "como ordenar uma lista em
TypeScript", lembre-se: **TypeScript é o ambiente de execução do JavaScript com
um verificador de tipos em tempo de compilação**.
A maneira de ordenar uma lista em TypeScript é a mesma que você usa em
JavaScript.
Se você encontrar um recurso que use TypeScript diretamente, ótimo também, mas
não se limite a pensar que precisa de respostas específicas de TypeScript para
perguntas comuns sobre como realizar tarefas em tempo de execução.

## Próximos passos

Esta foi uma breve visão geral da sintaxe e das ferramentas usadas no TypeScript
do dia a dia.
A partir daqui, você pode:

- Aprender alguns dos fundamentos do JavaScript.
  Recomendamos:

  - Os
    [Recursos de JavaScript da Microsoft](https://developer.microsoft.com/javascript/)
    ou;
  - O
    [Guia de JavaScript na Documentação Web da Mozilla](https://developer.mozilla.org/docs/Web/JavaScript/Guide).

- Continuar com
  [TypeScript para pessoas programadoras JavaScript](/docs/handbook/typescript-in-5-minutes.html);
- Ler o manual completo [do início ao fim](/docs/handbook/intro.html);
- Explorar os [Exemplos do Playground](/play#show-examples).

<!-- Nota: Terei prazer em escrever o seguinte... -->
<!--
## Tipos

  * O que é um tipo? (Para iniciantes);
    * Um tipo é um *tipo* de valor;
    * Os tipos definem implicitamente quais operações fazem sentido sobre eles;
    * Existem muitos tipos diferentes, não apenas primitivos;
    * Podemos criar descrições para todos os tipos de valores;
    * O tipo `any` -- uma breve descrição, o que é e por que é ruim.
  * Inferência 101;
    * Exemplos;
    * O TypeScript consegue inferir os tipos na maioria das vezes;
    * Dois lugares onde perguntaremos qual é o tipo: limites de função e valores
      inicializados posteriormente.
  * Aprendendo JavaScript em conjunto.
    * Você pode e deve ler recursos de JS existentes;
    * Basta colar e ver o que acontece;
    * Considere desativar o modo 'strict'.
-->
