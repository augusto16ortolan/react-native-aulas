---
description: >-
  Agora que entendemos um pouco sobre assincronismo, APIs e métodos/retornos
  HTTP, podemos colocar a mão no código.
---

# Vamos para a prática?

<figure><img src="../.gitbook/assets/8.jpg" alt=""><figcaption></figcaption></figure>

### Maneiras de declarar variáveis no Javascript

No Javascript, você pode declarar variáveis de três maneiras principais:

1. **`var`**: Declara uma variável com escopo de função ou global. É a forma mais antiga de declaração de variáveis e pode causar problemas com escopo e sobrescrita de variáveis.

```javascript
var nome = 'João';
```

2. **`let`**: Introduzido em 2015, declara uma variável com escopo de bloco, o que significa que é limitada ao bloco onde foi definida. Ideal para variáveis cujo valor muda ao longo do tempo.

```javascript
let idade = 30;
idade = 31; // Valor pode ser alterado
```

3. **`const`**: Também introduzido em 2015, declara uma variável com escopo de bloco, mas cujo valor não pode ser alterado depois de definido. Usado para constantes e referências que não devem mudar.

```javascript
const PI = 3.14;
// PI = 3.14159; // Erro: PI é uma constante
```

Cada método tem seu próprio comportamento e uso ideal, sendo `let` e `const` recomendados para a maioria dos casos modernos devido à sua clareza e controle de escopo mais preciso.

### Exemplos das declarações em funções

```javascript
function exemploVar() {
  var x = 10;
  if (true) {
    var x = 20; // Redeclaração
    console.log(x); // 20
  }
  console.log(x); // 20 (acessível fora do bloco if)
}
exemploVar();
```

Nesse primeiro exemplo, podemos ver uma maneira que não é mais recomendado utilizar a declaração do var, pois por conta da redeclaração da mesma variável, podemos causar sérios problemas nos códigos, onde precisamos manter um valor dentro de um bloco sem alterá-lo em outra parte do código.

```javascript
function exemploLet() {
  let y = 10;
  if (true) {
    let y = 20; // Nova variável, escopo do bloco
    console.log(y); // 20
  }
  console.log(y); // 10 (fora do bloco if)
}
exemploLet();
```

Já nesse segundo exemplo, usando let, não corremos o perigo de alterações de códigos indesejadas. Então, nos dias de hoje, usar a declaração let é altamente recomendada para manter um código muito bem estruturado.

### Exemplos de promises

Obejto que representa uma operação assíncrona:

```javascript
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Dados recebidos");
    }, 2000);
  });
}
```

Sintaxe para trabalhar com Promises de forma mais legível:

```javascript
async function getData() {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

getData();
```

#### Resolvendo a Promise

Para resolver uma Promise podemos utilizar a função resolve, passando como parâmetro um valor que será acessível através de nossa Promise resolvida:

```javascript
function fazRequisicao() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Promise resolvida");
    }, 5000);
  });
}
```

Veja que para simular uma requisição adicionei um setTimeout para aguardar cinco (5) segundos antes de resolver a Promise. Legal, nossa Promise está resolvida, mas como podemos pegar o valor passado para a função resolve? Para isso, podemos utilizar a função then das Promises, como foi mencionado no começo do post:

```javascript
fazRequisicao()
 .then(console.log);
```

Veja que ao realizar o then estamos fazendo um console.log, ou seja, estamos logando no console do navegador qualquer resposta que venha dentro de nossa função resolve. Após esperar cinco (5) segundos a mensagem de Promise resolvida deve ser impressa no console.

Reforçando: Qualquer valor passado para a função resolve será acessível como parâmetro da função .then, o valor pode ser uma String, Number, Booleano, Function (sim, podemos passar outra função), Object, etc…

#### Rejeitando a Promise

Assim como fizemos para resolver a Promise, também podemos rejeitá-la. Para realizar a simulação de rejeição será necessário fazer algumas modificações em nossa função, a primeira delas é adicionar um parâmetro informando se a Promise deve ser resolvida ou não:

```javascript
function fazRequisicao(resolver = true) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Promise resolvida");
    }, 5000);
  });
}
```

Também foi adicionado um valor padrão (default) para o parâmetro, ou seja, se o mesmo não for informado seu valor será true (verdadeiro) sendo assim precisamos fazer um pequeno if para tratar essa condição

```javascript
function fazRequisicao(resolver = true) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (!resolver) {
        // rejeitá-la
      }
      resolve("Promise resolvida");
    }, 5000);
  });
}
```

Veja que evitamos adicionar if e else, isso também é chamado de Early Return. Legal, as modificações estão prontas, agora podemos de fato rejeitá-la, isso pode ser feito de duas maneiras. 1º Utilizando a função reject (da mesma forma que a resolve):

```javascript
function fazRequisicao(resolver = true) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (!resolver) {
        reject("Deu erro");
      }
      resolve("Promise resolvida");
    }, 5000);
  });
}
```

Ou lançando um erro:

```javascript
function fazRequisicao(resolver = true) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (!resolver) {
        throw new Error("Deu erro");
      }
      resolve("Promise resolvida");
    }, 5000);
  });
}
```

Legal, ela foi resolvida e como podemos realizar esse tratamento? Assim como temos o then para sucesso, também temos o catch para erros

```javascript
fazRequisicao(false)
 .then(console.log)
 .catch(console.error);
```

### Exemplo utilizando fetch

API nativa do Javascript para fazer requisições HTTP:

```javascript
async function getAddress(cep) {
  try {
    const response = await fetch(`https://viacep.com.br/ws/${cep}/json/`);
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Erro:", error);
  }
}

getAddress("99560000");
```

### Exemplo utilizando axios

Existe uma maneira melhor para fazer requisições HTTP, usando uma biblioteca mais fácil de usar e com mais funcionalidades, o axios.

Primeiramente precisamos instalar essa biblioteca:

```javascript
npm install axios
```

Agora podemos usar a biblioteca:

```javascript
const axios = require("axios"); //Sempre deve ficar no cabeçalho do arquivo

async function getAddress(cep) {
  try {
    const response = await axios.get(`https://viacep.com.br/ws/${cep}/json/`);
    console.log(response.data);
  } catch (error) {
    console.error("Erro:", error);
  }
}

getAddress("01001000");
```

### Exemplos de tratamento de erros em códigos

Para manter um código bem estruturado e seguro para os usuários, devemos sempre nos prevenir e tratar erros.

No Javascript, a melhor maneira de se fazer isso é utilizando o bloco try/catch. Funciona bem como é a tradução, caso ocorra um erro dentro do bloco try, o erro é capturado dentro do catch, podendo ter o fim que o programador desejar.

Bloco try/catch:

```javascript
try {
  // Código que pode lançar uma exceção
} catch (erro) {
  // Código que será executado se uma exceção for lançada
  console.error(erro);
}
```

Código com erro, cairá no catch:

```javascript
const jsonString = '{"nome": "Jon Snow", "idade": 30'; // JSON malformado

try {
  const usuario = JSON.parse(jsonString);
  console.log(usuario.nome);
} catch (erro) {
  console.error("Erro ao analisar JSON:", erro.message);
}
```

Retorno definido pelo desenvolvedor:

```javascript
function dividir(a, b) {
  try {
    if (b === 0) {
      throw new Error("Divisão por zero não é permitida");
    }
    return a / b;
  } catch (erro) {
    console.error("Erro:", erro.message);
    return null;
  }
}

const resultado1 = dividir(10, 2);
console.log("Resultado da divisão:", resultado1); // 5

const resultado2 = dividir(10, 0);
console.log("Resultado da divisão:", resultado2); // null
```

Utilizando o finally, onde será executado sempre, mesmo caindo no catch:

```javascript
function lerArquivo() {
  try {
    console.log("Abrindo arquivo...");
    // Simula uma operação que pode lançar uma exceção
    throw new Error("Erro ao ler o arquivo");
  } catch (erro) {
    console.error("Erro:", erro.message);
  } finally {
    console.log("Fechando arquivo...");
  }
}

lerArquivo();
```

### Conclusão

Depois de explorar os tópicos abordados, adquirimos uma compreensão fundamental sobre a declaração de variáveis em Javascript, utilizando var, let e const. Também aprendemos a trabalhar com Promises, compreendendo como resolvê-las e rejeitá-las conforme necessário. Além disso, vimos como consumir APIs e realizar chamadas assíncronas usando fetch e axios, bem como as melhores práticas para tratamento de erros em códigos Javascript. Essa base sólida é essencial para construir aplicações robustas e eficazes, garantindo uma manipulação eficiente de dados e uma experiência de usuário fluida.
