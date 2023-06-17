# Programação Funcional

Assim como a Programação Orientada a Objetos, é um paradigma de programação, que é uma maneira de pensar e resolver problemas. O grande lance desse paradigma, são as **funções**, que guardam pequenas tarefas. Separamos problemas por tarefas pequenas. Sem modificar dados por fora dela, apenas dentro do escopo dela. Além de, serem bem pequenas e específicas no que fazer.

## Por que programação funcional?

Serve para organizar linhas de raciocínio, quando entendemos uma nova maneira de abordar problemas, automaticamente, melhoramos o entendimento do problema e de encontro à solução. Além de, algumas tecnologias tem a programação funcional como requisito.

## Características

Um dado (ou mais), entrará na função e um dado novo sai dela, um dado modificado. Não altera os dados e não guarda o estado, que chamamos de `stateless`.

Algumas linguagens funcionais são:

- JavaScript (multiparadigma)
- PHP (multiparadigma)
- Elixir
-

É uma linguagem de fácil manutenção, fácil para fazer testes, e também, deixa o código mais confiável.

## Princípios

- **Paradigmas**
  - Programação Imperativa
  - Programação Declarativa
- **Dados**
  - Imutabilidade
  - Stateless
- **Funções**
  - Funções Independentes
  - Funções Puras
  - Higher-order Functions
  - First-class Functions
  - Composição de Funções

## Programação Imperativa e Declarativa

### Imperativo

O modelo imperativo é como se fosse uma receita de bolo, nós instruímos ao computador passo a passo os comando que ele deve ensinar. Por exemplo:

```js
// Uma função que eleva o número ao quadrado
// De forma imperativa: Como fazer

let number = 2

function squared() {
  return number * n
}

number = squared()
```

Uma sequência de tarefas passo a passo. Linha a linha, fui falando como deve ser feito. Dar ordens.

### Declarativo

O modelo declarativo se concentra em descrever o que desejamos alcançar e deixar o computador se virar, ao invés de instruir especificamente ao computador o que queremos.

```js
// Uma função que eleva o número ao quadrado
// De forma declarativa: O que fazer
const squared = (n) => n * n
```

Uma função que eleva o número ao quadrado.

> Contudo, na programação imperativa damos todos os passos específicos, seguindo exatamente o que mandamos. Já na declarativa apenas dizemos onde queremos chegar e deixamos o computador se virar para dar o que queremos.

## Imutabilidade

Uma variável não vai variar. Estamos falando sobre constantes, que sã variáveis que não podem ser reescritas. Por exemplo: temos uma bola azul, não posso mudar a cor da bola para amarela, então, criaremos outra bola da cor amarela.

```js
const carrinho = {
  produtos: 2,
  preco_total: 30,
}

carrinho.produtos = 3
// isso não é possível de se fazer, o valor não pode ser alterado.

const novoCarrinho = { ...carrinho, produtos: 5 }
// isso é possível, uma nova variável que pegar os valores de outra e muda certas coisas
```

## Stateless

O conceito de **stateless** significa que algo não vai guardar o estado. No caso de funções, ela só vai conhecer os dados entregues a ela, e não vai pegar os dados de seu exterior. Pois, pode ser que a resposta dela varie.

- **state** = estado
- **less** = menos

Um exemplo:

```js
let number = 5

// stateful function
function squared() {
  return number * number
}

number = squared() // 25
number = squared() // 625

// stateless function
const squared = (n) => n * n
```

Vejamos que, em **stateful function**, a função utiliza o _number_ que está no seu exterior, contudo, no final `number = squared()`, a função vai sobrescrever o valor de _number_. Mas se chamarmos essa função novamente para sobrescrever _number_, o valor não será mais o mesmo. O que é um problema do **stateful function**

Já no **stateless function**, a função não vai guardar nenhum valor, apenas receberá um valor e sempre o `n * n` será o resultado. Portanto, a função em si, não está guardando nenhum estado. A função não sabe o valor de `n`, só vai saber quando for passado.

> Então, o segredo é que, não posso depender de dados externos, não posso guardar dados na função, não posso alterar dados externos. Só vou trabalhar com dados entregues para a minha função.

## Funções Independentes

Como o próprio nome já diz, não pegará dados externos, apenas os dados passados para ela como argumento, deverá ter ao menos 1 argumento, e sempre retornará algo.

Nada do que acontecer dentro da função, afetará o mundo externo, pois os dados são imutáveis e não guardará estado.

Não fazemos uso de loops, como for e while, mas se houver necessidade, utilizaremos a recursão para isso, que é a função chamando ela mesma.

Veja um exemplo:

```js
const random = (number, Math) => Math.floor(Math.random() * number)
// Número aleatório
// Sempre retorna algo

// Encontrar o fatorial de um número
const factorial = (x) => {
  // Se o número for igual a 0
  if (x === 0) {
    return 1
  }

  return x * factorial(x - 1) // Recursão
}
// Sempre retorna algo

const number = random(10, Math)
const factoredNumber = factorial(number)

console.log(number + "! =", factoredNumber)
```

Em resumo, funções independentes trabalham com os dados passados como argumentos e não têm dependências externas, não afeta nada no código externo e não fazemos uso de loops, mas sim de recursão.

## Funções Puras

As funções puras, assim como as independentes, não irão depender de nenhum dado externo, a não ser o que foi passado como argumento, além de, não afetar nada no código externo, sempre retornam o mesmo resultado para os mesmos argumentos, o que é conhecido como **determinismo**, e também são _stateless_ (não guardam estado). Veja:

```js
// Funções Puras
// Exemplo 1: Depende apenas do dados passados como argumento

function calculateCircumference(pi, radius) {
  return pi * (radius + radius)
}

calculateCircumference(Math.PI, 20) // 125.6637

// Exemplo 2: Não altera dados externos, cria uma novo dado

let otherPerson = {
  name: "Larissa Camargo",
  age: "Adulta",
}

function changeName(person, newName) {
  return { ...person, name: newName }
}

const newOtherPerson = changeName(otherPerson, "Larissa Mendonsa")

console.log(newOtherPerson)
// { name: 'Larissa Mendonsa', age: 'Adulta' }
console.log(otherPerson)
// { name: 'Larissa Camargo', age: 'Adulta' }
```

Essas são as características de funções puras, logo, também existem as funções impuras, aquelas que dependem de dados externos, altera dados externos e guarda o estado:

```js
// Funções Impuras
// Exemplo 1: Depende de dados externos
function calculateCircumference(radius) {
  return Math.PI * (radius + radius)
}

// Exemplo 2: Altera dados externos
let person = {
  name: "Rafael Almeida",
  age: "Jovem",
}

function changeName(name) {
  person.name = name
}
```

## First-class Function

As funções de primeira classe, podem estar em qualquer lugar, inclusive, como parâmetro de outras funções, tal função poderá ser entendida como uma variável.

```js
const sayMyName = () => console.log("Matheus")

const runMyFunction = (myFunc) => myFunc()
// Pega a função e a executa (conceito de funções declarativas)

runMyFunction(sayMyName)
// Poderá ser entendida como uma variável

runMyFunction(() => console.log("Hello, World!"))
// Passamos apenas funções

console.log(runMyFunction(Math.random))
```

`Math.random` é uma função, mas passamos ela como se fosse uma variável, para `runMyFunction` executá-la dessa forma: `Math.random()`.

## Higher-order Function (HOF)

As funções de ordem superior, ao contrário das _first-class function_, ao invés de serem recebidas como parâmetro de outras funções, as _Higher-order Function_ é a função que recebe as _first-class function_ como parâmetro, e também podem retornar outras funções como resultado.

```js
const number = [2, 4, 6, 8]

const square = (n) => n ** 2
// Pega o número e multiplica por ele mesmo

const squaredNumbers = number.map(square)
// Cria um novo array, com todos os números elevados ao quadrado

console.log(number) // [2, 4, 6, 8]
console.log(squaredNumbers) // [ 4, 16, 36, 64 ]
```

Nesse código, há um array de números, logo, pegamos esse array e criamos um novo, a partir do método `map()`, porém, esse método vai receber uma função que vai pegar cada número do array, e vai elevá-los ao quadrado (`const squaredNumbers = number.map(square)`).

```js
function avarage(...allGrades) {
  return function (fn) {
    console.log(fn(allGrades.length, allGrades))
  }
}

avarage(9, 7, 8, 10)((gradesLength, allGrades) => {
  let gradesSum = 0
  allGrades.forEach((grade) => {
    gradesSum += grade
  })
  return gradesSum / gradesLength
})
```

O `averageCalc` é uma função de ordem superior, pois tem a função `fn` como argumento e também retorna uma função.

Em resumo, as _Higher-order functions_ recebem outras funções como argumentos ou retornam outras funções como resultado.

## Currying

**Currying** ou **aplicação parcial de função**, em homenagem a Haskell Curry, que fundamentou o conceito de paradigma funcional.

Exemplo de **currying**:

```js
const sum = (n1) => (n2) => n1 + n2
console.log(sum(5)(4)) // 9
```

Basicamente, é uma forma cuja função recebe apenas uma função. Portanto, para fazer uma função com dois ou mais parâmetros fixos, aninhamos funções e colocamos um parâmetro para cada, e, por fim, retornando elas mesmas, `const sum = (n1) => (n2) => ...`, dessa forma.

E para usarmos essa função, em uma função normal colocamos `sum(5, 4)`, mas, no caso, usaremos `sum(5)(4)`, que significa que a primeira função recebe 5 como parâmetro `sum(5)`, e o segunda função, que não tem nome, recebe 4, `(4)`, junto à primeira função.

Contudo, na hora de executar essas funções, podemos adicionar um parâmetro por vez:

```js
const curry = (func) => (a) => (b) => func(a, b)

const sum = (n1, n2) => n1 + n2
const useCurryToSum = curry(sum)

console.log(useCurryToSum(5)(4))
```

Explicando:

- `const curry = (func) => a => b => func(a, b)`: essa função tem a funcionalidade de executar uma outra função que utiliza os parâmetro a e b, para alguma tarefa, resumidamente.

- `const sum = (n1, n2) => n1 + n2`: essa é a função que será passada ao `curry`.

- `const useCurryToSum = curry(sum) `: estamos aplicando o currying na função `sum`. E agora`useCurryToSum` é uma função que pode ser chamada com dois conjuntos de parênteses separados, permitindo passar os argumentos um por vez.

- `console.log(useCurryToSum(5)(4))`: dessa forma adicionamos os parâmetros 5 e 4, um por vez dentro da função useCurryToSum.
