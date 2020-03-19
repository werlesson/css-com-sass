# CSS com SASS

> Projeto desenvolvido para explorar os conceitos abordados no SASS.

<!-- [![NPM Version][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]
[![Downloads Stats][npm-downloads]][npm-url] -->

<!-- De um a dois parágrafos sobre o que é seu projeto e o que ele faz. -->

Este projeto é para o entendimento e apresentação do pré-processador CSS **SASS**. Há a exposição de alguns exemplos práticos sobre o uso do [SASS][sass] e definição de conceitos utilizados. Desta maneira, o objetivo é mostrar a facilidade no desenvolovimento de algum projeto _WEB_, no que condiz a estilização das páginas _HTML_.

![Alt](./img/header.png "Logo do SASS")

[https://sass-lang.com/][sass]

<!-- ## Objetivos -->

## Introdução

### O que é SASS

**SASS** é um pré-processador de CSS que adiciona capacidade de uma linguagem de programação no CSS.

### SASS vs SCSS

**SASS** foi a primeira forma de uso e é baseado na identação e ausência de chave e ponto e vírgula. Já o **SCSS** é mais parecido com o CSS, usando ponto e vírgula e chave. **SCSS** permite uma melhor visualização e evita erros baseados em identação incorreta.

SASS

```sass
div
  background-color: blue
  padding: 10px
  margin-left: 8px
  p
    line-height: 15px
```

SCSS

```scss
div {
  background-color: blue;
  padding: 10px;
  margin-left: 8px;
  p {
    line-height: 15px;
  }
}
```

## Instalar projeto

Abra a pasta do projeto pelo terminal e rode o seguinte comando:

```zsh
npm install
```

## Pré-processar

Para iniciar o pré-processamento, utilize o seguinte comando:

```zsh
npm run build
```

Para iniciar o pré-processamento de maneira comprimida, utilize o seguinte comando:

```zsh
npm run build-compressed
```

## Fundamentos

### Partials

Você pode criar arquivos Sass parciais que contêm pequenos trechos de CSS que podem ser incluídos em outros arquivos Sass. Essa é uma ótima maneira de modularizar seu CSS e ajudar a manter as coisas mais fáceis de manter. Parcial é um arquivo Sass nomeado com um sublinhado à esquerda. Você pode nomear algo como _\_partial.scss_. O sublinhado informa ao Sass que o arquivo é apenas um arquivo parcial e que não deve ser gerado em um arquivo CSS. As parciais sass são usadas com a regra **@use** ou **@import**.

---

### Import

O Sass estende a regra @import do CSS com a capacidade de importar folhas de estilo Sass e CSS, fornecendo acesso a mixins, funções e variáveis e combinando o CSS de várias folhas de estilo. Diferente das importações simples de CSS, que exigem que o navegador faça várias solicitações HTTP à medida que processa sua página, as importações do Sass são tratadas inteiramente durante a compilação.

Individual

```scss
@import "variables";
```

Múltiplos

```scss
@import "variables", "colors";
```

---

### Variáveis

Pense nas variáveis como uma maneira de armazenar as informações que você deseja reutilizar em toda a folha de estilo. Você pode armazenar itens como cores, pilhas de fontes ou qualquer valor CSS que achar que deseja reutilizar. Sass usa o símbolo \$ para transformar algo em variável. Aqui está um exemplo:

```scss
$font-stack: Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

---

### Nesting (Alinhamento)

O Sass permitirá aninhar seus seletores de CSS de uma maneira que segue a mesma hierarquia visual do seu HTML. Esteja ciente de que regras excessivamente aninhadas resultarão em CSS super qualificado que pode ser difícil de manter e geralmente é considerado uma má prática.

SCSS

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li {
    display: inline-block;
  }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

CSS

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

Para o uso do _:hover_, por exemplo, seria com o uso do _&_ :

```scss
nav {
  a {
    text-decoration: none;
    &:hover {
      opacity: 0.5;
    }
  }
}
```

---

### Mixin

Um mixin permite fazer grupos de declarações CSS que você deseja reutilizar em todo o site. Você pode até passar valores para tornar sua mixagem mais flexível.

#### Ajuda com prefixos

Um bom uso de um mixin é para prefixos de fornecedores. Aqui está um exemplo para _transform_.

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}
.box {
  @include transform(rotate(30deg));
}
```

#### Mixin dentro de Mixin

```scss
@mixin title {
  font-weight: bold;
  font-family: monospace;
}
@mixin text-large {
  font-size: 4em;
  line-height: 1;
}

@mixin title-large {
  @include title;
  @include text-large;
}

h1 {
  @include title-large;
}
```

#### Argumentos

```scss
@mixin color-text($color) {
  color: $color;
}

p {
  @include color-text(#ccc);
}
```

##### Mais argumentos

```scss
@mixin color-text($color, $size) {
  font-size: $size;
  color: $color;
}

p {
  @include color-text(#ccc, 12px);
}
```

##### Valor default

```scss
@mixin color-text($color, $size: 36px) {
  font-size: $size;
  color: $color;
}

p {
  @include color-text(#ccc);
}
```

##### Argumentos '...'

Todos os argumentos vão para um espaço só

```scss
@mixin box-shadow($shadow) {
  -webkit-box-shadow: $shadow;
  -ms-box-shadow: $shadow;
  box-shadow: $shadow;
}
.section {
  @include box-shadow(
    5px 5px 0 0 rgba(0, 0, 0, 0.5),
    5px 5px 0 0 rgba(0, 0, 0, 0.5),
    5px 5px 0 0 rgba(0, 0, 0, 0.5)
  );
}
```

#### Content

SCSS

```scss
@mixin mobile {
  @media (max-width: 600px) {
    @content;
  }
}

p {
  color: blue;
  @include mobile {
    color: green;
  }
}
```

CSS

```css
p {
  color: blue;
}

@media (max-width: 600px) {
  p {
    color: green;
  }
}
```

---

### Extend

Extende as propriedades de um item ao outro que recebe a extensão, da seguinte forma:

SCSS

```scss
.erro {
  color: red;
  font-weight: bold;
}

.button-erro {
  @extend .erro;
  color: blue;
  padding: 20px;
}
```

CSS

```css
.erro,
.button-erro {
  color: red;
  font-weight: bold;
}

.button-erro {
  color: blue;
  padding: 20px;
}
```

---

### Operadores

São utilizados os quatro operadores (soma, divisão, subtração, multiplicação e divisão) nas propriedades.

```scss
$altura: 10px;

p {
  font-size: 10px + 2;
  line-height: $altura * 2;
}
```

---

### Condicionais

controla se seu bloco é avaliado ou não (incluindo a emissão de estilos como CSS). A expressão geralmente retorna trueoufalse - se a expressão retornar true, o bloco será avaliado e, se a expressão retornar false, não será. _@if_, _@else if_ e _@else_.

```scss
@mixin triangle($size, $color, $direction) {
  height: 0;
  width: 0;

  border-color: transparent;
  border-style: solid;
  border-width: $size / 2;

  @if $direction == up {
    border-bottom-color: $color;
  } @else if $direction == right {
    border-left-color: $color;
  } @else if $direction == down {
    border-top-color: $color;
  } @else if $direction == left {
    border-right-color: $color;
  } @else {
    @error "Unknown direction #{$direction}.";
  }
}

.next {
  @include triangle(5px, black, right);
}
```

---

### Functions

Há funções nativas do sass e também há a possibilidade de criar novas funções. Entre as funções nativas, tem-se, por exemplo:

- lighten: Deixa a cor mais clara

```scss
a {
  background: lighten(#eee, 20%);
}
```

- darken: Deixa a cor mais escura

```scss
a {
  background: darken(#eee, 20%);
}
```

- transparentize: Manipula a opacidade da cor

```scss
a {
  background: transparentize(#eee, 20%);
}
```

- round: Arredonda para inteiro os valores em decimal

```scss
a {
  width: round(100px / 3);
}
```

#### Criar funções

Também há a possibilidade de criar funções, como no exemplo abaixo:

```scss
@function em($pixels, $contexto: 16) {
  @return ($pixels / $contexto) * 1em;
}

p {
  font-size: em(24px); // return 1.5em;
}
```

---

### Controle de Fluxo

#### @while

Avalia seu bloco se sua expressão retornar true. Então, se sua expressão ainda retornar true, ele avaliará seu bloco novamente. Isso continua até que a expressão finalmente retorne false.

```scss
$i: 1;

@while $i <=6 {
  .type-#{$i} {
    font-size: 16 8 $i + px;
  }
  $i: $i + 1;
}
```

#### @for

Conta para cima ou para baixo de um número (o resultado da primeira expressão ) para outro (o resultado da segunda) e avalia um bloco para cada número intermediário. Cada número ao longo do caminho é atribuído ao nome da variável. Se tofor usado, o número final é excluído; se throughfor usado, está incluído.

```scss
@for $i from 1 through 6 {
  .item-#{$i} {
    width: 100px * $i;
  }
}
```

#### @each

Facilita a emissão de estilos ou a avaliação do código para cada elemento de uma lista ou cada par em um mapa . É ótimo para estilos repetitivos que têm apenas algumas variações entre eles. Geralmente é escrito _@each \<variable> in \<expression> { ... }_, onde a expressão retorna uma lista. O bloco é avaliado para cada elemento da lista, por sua vez, atribuído ao nome da variável.

```scss
$sizes: 40px, 50px, 80px;

@each $size in $sizes {
  .icon-#{$size} {
    font-size: $size;
    height: $size;
    width: $size;
  }
}
```

<!-- ## Instalação

OS X & Linux:

```sh
npm install my-crazy-module --save
````

Windows:

````sh
edit autoexec.bat
``` -->

<!-- ## Exemplo de uso

Alguns exemplos interessantes e úteis sobre como seu projeto pode ser utilizado. Adicione blocos de códigos e, se necessário, screenshots.

_Para mais exemplos, consulte a [Wiki][wiki]._ -->

<!-- ## Configuração para Desenvolvimento

Descreva como instalar todas as dependências para desenvolvimento e como rodar um test-suite automatizado de algum tipo. Se necessário, faça isso para múltiplas plataformas.

```sh
make install
npm test
``` -->

<!-- ## Histórico de lançamentos

- 0.2.1
  - MUDANÇA: Atualização de docs (código do módulo permanece inalterado)
- 0.2.0
  - MUDANÇA: Remove `setDefaultXYZ()`
  - ADD: Adiciona `init()`
- 0.1.1
  - CONSERTADO: Crash quando chama `baz()` (Obrigado @NomeDoContribuidorGeneroso!)
- 0.1.0
  - O primeiro lançamento adequado
  - MUDANÇA: Renomeia `foo()` para `bar()`
- 0.0.1
  - Trabalho em andamento -->

## Meta

Werlesson Vieira – [@werlessonvieira](https://twitter.com/werlessonvieira) – werlessono@gmail.com

Distribuído sob a licença [MIT][mit]. Veja `LICENSE` para mais informações.

[https://github.com/werlesson](https://github.com/werlesson)

[npm-image]: https://img.shields.io/npm/v/datadog-metrics.svg?style=flat-square
[npm-url]: https://npmjs.org/package/datadog-metrics
[npm-downloads]: https://img.shields.io/npm/dm/datadog-metrics.svg?style=flat-square
[travis-image]: https://img.shields.io/travis/dbader/node-datadog-metrics/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/dbader/node-datadog-metrics
[wiki]: https://github.com/seunome/seuprojeto/wiki
[mit]: https://choosealicense.com/licenses/mit/
[sass]: https://sass-lang.com/
