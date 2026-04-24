---
description: >-
  Nesta seção, vamos iniciar a prática com Javascript e Node.js, aplicando os
  conceitos iniciais da programação.
---

# Vamos para a prática?

<figure><img src="../.gitbook/assets/React Native (2).png" alt=""><figcaption></figcaption></figure>

### Imprimindo mensagens

```javascript
console.log("Hello world!");
```

O `console.log` é uma das funções mais básicas e úteis em Javascript, utilizada principalmente para exibir informações no console do navegador ou do ambiente de desenvolvimento. Essa função é fundamental para depuração e para fornecer feedback durante o desenvolvimento.

### Tipagens

```javascript
console.log(typeof "1"); //string
console.log(typeof 1); //number
console.log(typeof 1.0); //number
console.log(typeof true); //boolean

lista = [1, 2, 3, 4 ,5]
console.log(typeof lista); //object

pessoa = {
    name: "Jhon Snow"
}
console.log(typeof pessoa); //object
```

**String**: Representa uma sequência de caracteres.\
**Number**: Representa números, tanto inteiros quanto de ponto flutuante.\
**Boolean**: Representa valores lógicos, verdadeiro (`true`) ou falso (`false`).\
**Array**: Em Javascript, arrays são tecnicamente objetos, mas são usados para armazenar listas ordenadas de valores.\
**Object**: Representa coleções de pares chave-valor e pode ser usado para armazenar dados estruturados.\
\
Entender os tipos de dados e como usar a função `typeof` ajuda a escrever código mais robusto e a evitar erros comuns. Lembre-se de que, enquanto `typeof` é útil para identificar tipos primitivos e objetos, verificar arrays e nulos pode exigir métodos adicionais.

### Estruturas de condição

#### If, else if e else

```javascript
num = 10;
if (num > 0) {
    console.log('Número positivo');
} else if (num < 0) {
    console.log('Número negativo');
} else {
    console.log('Zero');
}
```

As estruturas condicionais `if`, `else if` e `else` permitem que você controle o fluxo do seu programa com base em condições específicas. Usar essas estruturas de maneira eficaz é essencial para criar lógica condicional em seus scripts Javascript.

#### Switch case

```javascript
num = 20;
switch(num) {
    case 10:
        console.log('O número é 10');
        break;
    case 20:
        console.log('O número é 20');
        break;
    default:
        console.log('Outro número');
}
```

A estrutura `switch` é útil quando você precisa comparar uma variável com múltiplos valores possíveis e executar diferentes blocos de código com base no valor correspondente. Ela oferece uma maneira mais organizada e legível de lidar com múltiplas condições em comparação com uma série de instruções `if` e `else if`.

### Laços de repetição

#### While

```javascript
i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

O `while` é uma ferramenta poderosa para realizar repetições baseadas em condições. É ideal para cenários onde o número de iterações não é conhecido antecipadamente e depende de uma condição que deve ser verificada a cada iteração.

#### For

```javascript
for (j = 0; j < 5; j++) {
    console.log(j);
}
```

O `for` é uma estrutura de repetição versátil e eficiente para executar um bloco de código um número específico de vezes. É especialmente útil quando o número de iterações é conhecido antecipadamente ou quando se trabalha com estruturas de dados iteráveis, como arrays.

#### For...in

```javascript
objeto = {a: 1, b: 2, c: 3};
for (chave in objeto) {
    console.log(chave, objeto[chave]);
}
```

O `for...in` é uma ferramenta útil para iterar sobre as propriedades de um objeto, permitindo acessar e manipular as chaves e valores do objeto de forma dinâmica. É importante ter cuidado com a herança de propriedades e com a ordem das propriedades ao usar `for...in`.

#### For...of

```javascript
lista = [1, 2, 3, 4, 5];
for (valor of lista) {
    console.log(valor);
}
```

O `for...of` é uma estrutura de repetição moderna e intuitiva para iterar sobre os valores de coleções iteráveis. É especialmente útil para trabalhar com arrays e outras estruturas de dados que implementam o protocolo de iteração, oferecendo uma maneira clara e direta de acessar e processar valores.

### Funções

#### Declaração tradicional

```javascript
function soma(a, b) {
    return a + b;
}

console.log(soma(2, 3)); 
```

A declaração tradicional de funções em Javascript é uma das formas mais comuns de definir uma função. Ela permite encapsular um bloco de código que pode ser executado quando a função é chamada. As funções definidas desta forma são "hoisted", o que significa que podem ser usadas antes de sua declaração no código.

#### Arrow function

```javascript
const subtrai = (a, b) => a - b;

console.log(subtrai(5, 2)); 
```

As arrow functions oferecem uma maneira simplificada e mais elegante de definir funções em JavaScript. Elas são ideais para funções pequenas e para manter o contexto léxico de `this`, tornando o código mais limpo e fácil de entender.

## Conclusão

Compreender e utilizar eficientemente essas estruturas de repetição e formas de declarar funções é essencial para escrever código Javascript claro, conciso e robusto. Esses conceitos são fundamentais para o desenvolvimento de aplicações modernas e serão aplicados em projetos práticos com Node.js, consolidando nosso aprendizado através da prática.
