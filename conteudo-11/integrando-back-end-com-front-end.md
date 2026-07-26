# Integrando Back-end com Front-end

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Quando o aplicativo deixa de ser apenas uma interface e passa a trabalhar com dados reais, ele precisa se comunicar com um back-end.

Essa integração acontece, na maior parte do tempo, por meio de:

* requisições HTTP;
* APIs REST;
* autenticação;
* tratamento de resposta e erro.

## O papel da API

A API funciona como uma ponte entre o app e o servidor.

Por ela, o aplicativo pode:

* buscar dados;
* enviar formulários;
* autenticar usuários;
* atualizar informações;
* remover registros.

## Estrutura básica de uma requisição

Toda requisição costuma envolver:

* **URL**
* **método HTTP**
* **headers**
* **body**, quando necessário

Exemplo:

```javascript
await fetch("https://api.exemplo.com/tasks", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer TOKEN_EXEMPLO",
  },
  body: JSON.stringify({
    title: "Estudar navegação",
  }),
});
```

## Ferramentas comuns no React Native

### `fetch`

É nativo do JavaScript e já resolve muita coisa.

### `axios`

É muito usado porque simplifica:

* configuração de base URL;
* interceptadores;
* tratamento de resposta;
* organização de serviços.

### Serviços separados

Em projetos maiores, vale criar arquivos como:

* `services/api.js`
* `services/tasks.js`
* `services/auth.js`

Isso evita espalhar lógica de requisição em toda tela.

## Segurança na comunicação

Algumas regras precisam virar hábito:

* use `https://`;
* valide os dados enviados;
* trate respostas de erro;
* não exponha segredos do servidor no app;
* use tokens apenas quando o fluxo pedir autenticação.

## Exemplo de organização com Axios

`src/services/api.js`

```javascript
import axios from "axios";

export const api = axios.create({
  baseURL: process.env.EXPO_PUBLIC_API_URL,
  headers: {
    "Content-Type": "application/json",
  },
});
```

Depois, em uma tela:

```javascript
const response = await api.get("/tasks");
```

## Fluxo típico de integração

1. o usuário faz uma ação no app;
2. a tela envia uma requisição;
3. o back-end processa;
4. a resposta volta;
5. a interface atualiza.

## Conclusão

A integração entre front-end e back-end é o que transforma uma interface estática em um aplicativo funcional. Entender esse fluxo é essencial para que os próximos exemplos de CRUD façam sentido do começo ao fim.
