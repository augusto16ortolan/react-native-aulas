---
description: >-
  Como lidar com falhas em operações assíncronas no JavaScript e no Node.js sem
  quebrar a aplicação
---

# Tratamento de erros no JavaScript

<figure><img src="../.gitbook/assets/ChatGPT Image 2 de fev. de 2026, 22_08_32.png" alt=""><figcaption></figcaption></figure>

Em JavaScript (e principalmente no **Node.js**), é comum trabalharmos com tarefas que não terminam imediatamente, como **chamadas a APIs**, **leitura de arquivos**, **consultas em banco** e outras operações de I/O. Como essas ações dependem de fatores externos (rede, permissões, disponibilidade de serviços, dados corretos), elas podem **falhar**, e é aí que entra o **tratamento de erros**: garantir que o sistema continue previsível, mesmo quando algo dá errado.

### O que é um erro no JavaScript?

Um erro é uma condição que impede o fluxo “normal” do programa. Em JavaScript, erros geralmente são representados por um objeto do tipo **`Error`**, que costuma trazer informações importantes para depuração:

* `message`: mensagem do erro
* `name`: tipo do erro (ex.: `TypeError`, `ReferenceError`)
* `stack`: rastreio do ponto onde ocorreu (muito útil no debug)

Exemplos comuns para iniciantes:

* **`TypeError`**: tentar acessar algo que não existe (ex.: `undefined.nome`)
* **`ReferenceError`**: usar variável que não foi declarada

### Diferença entre erro síncrono e assíncrono

#### Erro síncrono (acontece “na hora”)

O `try/catch` captura imediatamente:

```js
try {
  const pessoa = null;
  console.log(pessoa.nome); // TypeError
} catch (erro) {
  console.log("Erro síncrono:", erro.message);
}
```

#### Erro assíncrono (acontece “depois”)

Como a falha pode ocorrer em outro momento, usamos mecanismos ligados a **Promises** ou `async/await`.

### Por que tratar erros?

Tratar erros ajuda a:

* Evitar que a aplicação **trave** ou pare de responder
* Criar comportamentos **previsíveis** (mesmo em falhas)
* Deixar logs mais claros para **corrigir problemas**
* Melhorar a experiência do usuário (mensagens compreensíveis)

### Formas de tratar erros em chamadas assíncronas

#### A) Promises: `.then()` e `.catch()`

Se a Promise falhar, ela é **rejeitada** e vai para o `.catch()`.

```js
buscarUsuario()
  .then((usuario) => {
    console.log("Usuário:", usuario);
  })
  .catch((erro) => {
    console.error("Erro ao buscar usuário:", erro.message);
  });
```

**Ideia-chave:**

* `.then()` = sucesso
* `.catch()` = falha

#### B) `async/await`: `try/catch`

No `async/await`, uma Promise rejeitada se comporta como um erro “lançado”, então o `catch` captura.

```js
async function listarUsuarios() {
  try {
    const usuarios = await buscarUsuarios();
    console.log("Usuários:", usuarios);
  } catch (erro) {
    console.error("Falha ao listar usuários:", erro.message);
  }
}
```

**Ideia-chave:** `await` espera o resultado; se falhar, dispara erro.

### Tratar ou propagar o erro?

Nem sempre a melhor decisão é “resolver” o erro onde ele acontece. Existem dois caminhos:

#### Tratar (resolver ali mesmo)

Você registra e devolve algo padrão.

```js
async function carregarConfig() {
  try {
    return await lerConfig();
  } catch (erro) {
    console.log("Config não encontrada, usando padrão.");
    return { modo: "padrao" };
  }
}
```

#### Propagar (repassar para quem chamou)

Você repassa o erro para alguém tomar decisão (ex.: camada de API/rota).

```js
async function buscarDados() {
  try {
    return await chamarServicoExterno();
  } catch (erro) {
    throw new Error("Serviço externo indisponível.");
  }
}
```

### Um cuidado importante: Promise “sem tratamento”

Se uma Promise falhar e ninguém capturar, pode surgir um erro do tipo **Unhandled Promise Rejection** e, dependendo do ambiente, sua aplicação pode ficar instável.

Por isso, regra simples para iniciantes:

* Se usou **Promise**, tenha `.catch()`
* Se usou **await**, tenha `try/catch`

### Conclusão

O tratamento de erros em JavaScript é essencial para manter o código **robusto e confiável**, especialmente em operações assíncronas muito comuns no Node.js. Ao usar **`.catch()` em Promises** ou **`try/catch` com `async/await`**, você garante que falhas (rede, dados inválidos, serviços indisponíveis) não derrubem a aplicação e que o sistema responda de forma clara e previsível. Em resumo: **código assíncrono bem feito sempre considera o que acontece quando algo dá errado**.
