---
description: >-
  Agora que vimos assincronismo, APIs e tratamento de erros, vamos praticar com
  exemplos diretos.
---

# Vamos para a prática?

<figure><img src="../.gitbook/assets/8.jpg" alt=""><figcaption></figcaption></figure>

## `let`, `const` e `var`

```javascript
var nomeAntigo = "João";
let idade = 30;
const curso = "React Native";
```

Para código moderno, prefira:

* `const` por padrão
* `let` quando o valor precisar mudar
* `var` apenas para entender código legado

## Promise simples

```javascript
function buscarMensagem() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Mensagem recebida");
    }, 1000);
  });
}

buscarMensagem().then(console.log);
```

## `async/await`

```javascript
async function executar() {
  const resultado = await buscarMensagem();
  console.log(resultado);
}

executar();
```

## Exemplo com `fetch`

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

getAddress("01001000");
```

## Exemplo com Axios

```javascript
const axios = require("axios");

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

## `try/catch`

```javascript
try {
  const usuario = JSON.parse('{"nome":"Ana"}');
  console.log(usuario.nome);
} catch (erro) {
  console.error("Erro ao analisar JSON:", erro.message);
}
```

## Conclusão

Esses exemplos já formam uma base muito útil para o que vem depois em React Native: chamadas de API, formulários, feedback de erro e carregamento de dados.
