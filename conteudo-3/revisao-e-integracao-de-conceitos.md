---
description: >-
  Revisite e consolide os conceitos aprendidos, e veja como integrá-los de
  maneira prática em seus projetos.
---

# Revisão e integração de conceitos

<figure><img src="../.gitbook/assets/ChatGPT Image 2 de fev. de 2026, 22_11_22.png" alt=""><figcaption></figcaption></figure>

Agora que aprendemos o básico do Javascript, podemos avançar um pouco mais em nossos estudos. Vamos integrar todos os conceitos que aprendemos até agora e melhorar ainda mais nosso desenvolvimento com a linguagem.

### Objetivos

1. **Revisar Conceitos Anteriores**: Consolidar o conhecimento dos conceitos básicos de JavaScript que aprendemos.
2. **Manipulação Avançada de Arrays e Objetos**: Explorar técnicas avançadas como `map`, `filter`, e `reduce` para manipular arrays, além de técnicas de destruturação.
3. **Modularização do Código**: Entender e aplicar a modularização em JavaScript usando `import` e `export`.

### Revisão dos conceitos básicos

Antes de prosseguirmos, vamos revisar brevemente os conceitos que aprendemos até agora:

* **Declaração de Variáveis**: `let`, `const`, e `var`
* **Estruturas Condicionais**: `if`, `else`, `switch`
* **Loops**: `while`, `for`, `for...in`, `for...of`
* **Funções**: Tradicionais e Arrow Functions
* **Boas Práticas**: Convenções de nomeação e manutenção de um código limpo e legível

### Manipulação de Arrays e Objetos

#### Métodos de Arrays

*   **`map`**: Imagine que você tem uma lista de frutas e quer transformar cada uma dessas frutas em suco. Com `map`, você pega cada fruta da lista, faz o suco e coloca em uma nova lista de sucos. Assim, `map` é como uma máquina que transforma cada item de uma lista em algo novo, mantendo a mesma quantidade de itens.

    Lista de frutas: `['maçã', 'banana', 'laranja']`

    Usando `map` para transformar em sucos: `['suco de maçã', 'suco de banana', 'suco de laranja']`

```javascript
const frutas = ['maçã', 'banana', 'laranja'];
const sucos = frutas.map(fruta => `suco de ${fruta}`);
console.log(sucos);
// Saída: ['suco de maçã', 'suco de banana', 'suco de laranja']
```

* **`filter`**: Agora imagine que você tem uma cesta cheia de frutas, mas quer separar apenas as frutas vermelhas. Com `filter`, você vai passar por cada fruta e só pegar aquelas que são vermelhas, colocando em uma nova cesta. Assim, `filter` é como uma peneira que só deixa passar os itens que atendem a um certo critério.\
  Lista de frutas: `['maçã', 'banana', 'morango', 'laranja']`\
  Usando `filter` para pegar apenas as frutas vermelhas: `['maçã', 'morango']`

```javascript
const frutas = ['maçã', 'banana', 'morango', 'laranja'];
const frutasVermelhas = frutas.filter(fruta => fruta === 'maçã' || fruta === 'morango');
console.log(frutasVermelhas);
// Saída: ['maçã', 'morango']
```

* **`reduce`**: Pense que você tem uma coleção de moedas e quer contar o valor total delas. Com `reduce`, você pega cada moeda e adiciona ao total acumulado, até contar todas as moedas. Assim, `reduce` é como um contador que pega uma lista de itens e reduz a um único valor, somando, multiplicando, ou combinando de alguma forma.\
  Lista de moedas: `[1, 2, 5, 10]`\
  Usando `reduce` para somar o valor total: `1 + 2 + 5 + 10 = 18`

```javascript
const moedas = [1, 2, 5, 10];
const valorTotal = moedas.reduce((total, moeda) => total + moeda, 0);
console.log(valorTotal);
// Saída: 18
```

Resumindo, o map transforma cada item de uma lista em algo novo, o filter seleciona apenas os itens que atendem a um certo critério e o reduce combina todos os itens de uma lista em um único valor.

#### Destruturação

* **Arrays**: Imagine que você tem uma lista de ingredientes para uma receita e quer pegar os dois primeiros ingredientes dessa lista de forma fácil.\
  Lista de ingredientes: `['farinha', 'açúcar', 'ovos', 'leite']`\
  Com a destruturação de arrays, você pode pegar os dois primeiros ingredientes assim:

```javascript
const ingredientes = ['farinha', 'açúcar', 'ovos', 'leite'];
const [primeiroIngrediente, segundoIngrediente] = ingredientes;
console.log(primeiroIngrediente); // Saída: 'farinha'
console.log(segundoIngrediente); // Saída: 'açúcar'
```

Aqui, estamos "destruturando" o array `ingredientes` e pegando os dois primeiros itens diretamente em variáveis chamadas `primeiroIngrediente` e `segundoIngrediente`.

* **Objetos:** Agora, imagine que você tem um cartão de contato com informações sobre uma pessoa e quer pegar apenas o nome e a cidade dessa pessoa de forma fácil.\
  Cartão de contato: `{ nome: 'João', idade: 30, cidade: 'São Paulo' }`\
  Com a destruturação de objetos, você pode pegar o nome e a cidade assim:

```javascript
const contato = { nome: 'João', idade: 30, cidade: 'São Paulo' };
const { nome, cidade } = contato;
console.log(nome); // Saída: 'João'
console.log(cidade); // Saída: 'São Paulo'
```

Aqui, estamos "destruturando" o objeto `contato` e pegando os valores das propriedades `nome` e `cidade` diretamente em variáveis com os mesmos nomes.

Resumindo, a destruturação de arrays facilita pegar itens específicos de uma lista, já a destruturação de objetos facilita pegar propriedades específicas de um objeto.

### Modularização

Imagine que você está construindo uma casa. Em vez de construir tudo de uma vez, você divide o trabalho em partes menores e gerenciáveis, como a fundação, as paredes, o telhado, etc. Cada parte é construída separadamente e depois junta-se para formar a casa completa. Isso facilita o trabalho, torna mais fácil encontrar e corrigir problemas, e permite que diferentes pessoas trabalhem em diferentes partes ao mesmo tempo.

Na programação, a modularização funciona da mesma forma. Em vez de escrever todo o código em um único arquivo enorme, você divide o código em partes menores e mais gerenciáveis chamadas "módulos". Cada módulo tem uma responsabilidade específica e pode ser desenvolvido, testado e mantido separadamente.

A modularização permite organizar melhor o código, facilitando a manutenção e a reutilização. Vamos aprender a criar módulos e a utilizá-los com `import` e `export`.

* **Criando um módulo (`math.js`)**:\
  Primeiro, criamos um arquivo chamado `math.js` que conterá nossas funções matemáticas:

```javascript
export const add = (a, b) => a + b;
export const subtract = (a, b) => a - b;
```

Aqui, estamos definindo duas funções, `add` (para adicionar) e `subtract` (para subtrair), e exportando-as para que possam ser usadas em outros arquivos.

* **Importando um módulo**:\
  Agora, criamos um arquivo principal chamado `main.js` que vai importar e usar essas funções:

```javascript
import { add, subtract } from './math.js';

console.log(add(5, 3)); // 8
console.log(subtract(5, 3)); // 2
```

Aqui, estamos importando as funções `add` e `subtract` do arquivo `math.js` e usando-as para realizar cálculos.

### Conclusão

O aprendizado contínuo e a prática são chave para se tornar proficiente em Javascript. Ao dominar esses conceitos, você não só melhora suas habilidades técnicas, mas também se prepara para enfrentar desafios mais complexos no desenvolvimento de software.
