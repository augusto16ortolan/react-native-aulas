---
description: >-
  Entenda como o JavaScript lida com tarefas assíncronas e por que isso é tão
  importante em aplicativos.
---

# Assincronismo e o Javascript

<figure><img src="../.gitbook/assets/6.jpg" alt=""><figcaption></figcaption></figure>

Em aplicativos, várias ações não terminam imediatamente:

* buscar dados da internet;
* salvar no banco;
* esperar resposta de uma API;
* acessar arquivos;
* aguardar um timer.

É aí que entra o **assincronismo**.

## Síncrono x assíncrono

### Síncrono

Cada linha espera a anterior terminar.

```javascript
console.log("Início");
console.log("Processando...");
console.log("Fim");
```

### Assíncrono

Uma tarefa longa pode ser iniciada enquanto o restante do código continua.

```javascript
console.log("Início");

setTimeout(() => {
  console.log("Resposta recebida depois");
}, 2000);

console.log("Fim");
```

Saída esperada:

1. `Início`
2. `Fim`
3. `Resposta recebida depois`

## Promises

Uma Promise representa o resultado futuro de uma operação assíncrona.

```javascript
function buscarDados() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Dados carregados");
    }, 2000);
  });
}

buscarDados().then((resultado) => {
  console.log(resultado);
});
```

## `async/await`

`async/await` deixa a leitura mais parecida com fluxo sequencial.

```javascript
function buscarDados() {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Dados carregados");
    }, 2000);
  });
}

async function carregarTela() {
  console.log("Carregando...");
  const resultado = await buscarDados();
  console.log(resultado);
}

carregarTela();
```

## Onde isso aparece no React Native

Assincronismo aparece o tempo todo em:

* `fetch` e `axios`;
* login;
* upload de imagem;
* leitura de armazenamento local;
* integração com Supabase.

## Conclusão

Entender assincronismo é essencial para não travar a interface e para organizar corretamente chamadas de API e operações de dados. Em mobile, isso não é detalhe: é parte do funcionamento normal do app.
