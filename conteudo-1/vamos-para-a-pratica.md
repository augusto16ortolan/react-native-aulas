---
description: >-
  Nesta seção, vamos praticar os fundamentos do JavaScript que serão usados em
  todo o restante do curso.
---

# Vamos para a prática?

<figure><img src="../.gitbook/assets/React Native (2).png" alt=""><figcaption></figcaption></figure>

Antes de entrar no React Native, vamos revisar alguns blocos essenciais da linguagem. Todos os exemplos abaixo funcionam em JavaScript moderno e seguem um padrão mais próximo do que vamos usar nos projetos.

### Imprimindo mensagens

```javascript
console.log("Hello world!");
console.log("Bem-vindo ao curso de desenvolvimento de aplicativos.");
```

`console.log()` é útil para inspecionar valores, entender o fluxo do programa e depurar problemas durante o desenvolvimento.

### Tipos de dados

```javascript
console.log(typeof "1"); // string
console.log(typeof 1); // number
console.log(typeof true); // boolean

const lista = [1, 2, 3, 4, 5];
console.log(typeof lista); // object

const pessoa = {
  nome: "John Snow",
  idade: 28,
};
console.log(typeof pessoa); // object
```

Pontos importantes:

* `string`, `number` e `boolean` são tipos básicos.
* arrays e objetos aparecem como `object` no `typeof`.
* em código moderno, prefira `const` por padrão e use `let` quando o valor realmente precisar mudar.

### Estruturas de condição

#### `if`, `else if` e `else`

```javascript
const numero = 10;

if (numero > 0) {
  console.log("Número positivo");
} else if (numero < 0) {
  console.log("Número negativo");
} else {
  console.log("Zero");
}
```

#### `switch`

```javascript
const statusPedido = "enviado";

switch (statusPedido) {
  case "novo":
    console.log("Pedido recém-criado");
    break;
  case "enviado":
    console.log("Pedido em transporte");
    break;
  default:
    console.log("Status não mapeado");
}
```

### Laços de repetição

#### `while`

```javascript
let i = 0;

while (i < 3) {
  console.log("while:", i);
  i++;
}
```

#### `for`

```javascript
for (let j = 0; j < 3; j++) {
  console.log("for:", j);
}
```

#### `for...in`

```javascript
const usuario = { nome: "Ana", cidade: "Passo Fundo" };

for (const chave in usuario) {
  console.log(chave, usuario[chave]);
}
```

Use `for...in` para percorrer **chaves de objetos**.

#### `for...of`

```javascript
const tecnologias = ["JavaScript", "React", "React Native"];

for (const tecnologia of tecnologias) {
  console.log(tecnologia);
}
```

Use `for...of` para percorrer **valores de coleções iteráveis**, como arrays.

### Funções

#### Declaração tradicional

```javascript
function soma(a, b) {
  return a + b;
}

console.log(soma(2, 3));
```

#### Arrow function

```javascript
const subtrai = (a, b) => {
  return a - b;
};

console.log(subtrai(5, 2));
```

Se a função tiver apenas uma expressão de retorno, ela pode ser encurtada:

```javascript
const multiplica = (a, b) => a * b;
```

### Arrays e objetos no dia a dia

```javascript
const tarefas = [
  { id: 1, titulo: "Estudar JavaScript", concluida: false },
  { id: 2, titulo: "Criar primeira tela", concluida: true },
];

console.log(tarefas[0].titulo);
console.log(tarefas[1].concluida);
```

Esse formato aparece o tempo todo em aplicativos, APIs e listas renderizadas em tela.

## Conclusão

Esses exemplos parecem simples, mas formam a base de quase tudo o que vamos construir depois: componentes, listas, estados, formulários, chamadas de API e navegação. Quanto mais natural ficar essa leitura em JavaScript, mais leve será o avanço no React Native.
