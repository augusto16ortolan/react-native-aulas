---
description: Entenda APIs, métodos HTTP e códigos de status no contexto de apps
---

# APIs e Métodos/Retornos HTTP

<figure><img src="../.gitbook/assets/7.jpg" alt=""><figcaption></figcaption></figure>

Uma API permite que o aplicativo converse com outro sistema. Em React Native, isso acontece o tempo todo quando buscamos dados ou enviamos informações para um servidor.

## Métodos HTTP mais comuns

* **GET**: buscar dados
* **POST**: criar dados
* **PUT**: substituir um recurso existente
* **PATCH**: atualizar parcialmente
* **DELETE**: remover dados

## Códigos de status importantes

* **200 OK**: requisição bem-sucedida
* **201 Created**: recurso criado com sucesso
* **400 Bad Request**: requisição inválida
* **401 Unauthorized**: autenticação ausente ou inválida
* **404 Not Found**: recurso não encontrado
* **500 Internal Server Error**: erro no servidor

## Exemplo com `GET`

```javascript
async function obterUsuarios() {
  try {
    const resposta = await fetch("https://jsonplaceholder.typicode.com/users");

    if (!resposta.ok) {
      throw new Error(`Falha HTTP: ${resposta.status}`);
    }

    const dados = await resposta.json();
    console.log(dados);
  } catch (erro) {
    console.error("Erro ao obter usuários:", erro.message);
  }
}
```

## Exemplo com `POST`

```javascript
async function criarUsuario() {
  try {
    const resposta = await fetch("https://jsonplaceholder.typicode.com/users", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        name: "João Silva",
        email: "joao@email.com",
      }),
    });

    if (!resposta.ok) {
      throw new Error(`Falha HTTP: ${resposta.status}`);
    }

    const dados = await resposta.json();
    console.log("Usuário criado:", dados);
  } catch (erro) {
    console.error("Erro ao criar usuário:", erro.message);
  }
}
```

## Conclusão

Saber o que é uma API, quais métodos HTTP usar e como interpretar os status de resposta facilita muito a construção de apps que consomem dados de forma correta e previsível.
