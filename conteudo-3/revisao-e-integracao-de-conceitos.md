---
description: >-
  Consolide os fundamentos de JavaScript que serão reaproveitados nas telas e
  integrações do aplicativo.
---

# Revisão e integração de conceitos

<figure><img src="../.gitbook/assets/ChatGPT Image 2 de fev. de 2026, 22_11_22.png" alt=""><figcaption></figcaption></figure>

Agora que a base da linguagem já foi apresentada, vale revisar alguns recursos que aparecem o tempo todo em React Native.

## Arrays: `map`, `filter` e `reduce`

```javascript
const tarefas = [
  { id: 1, titulo: "Estudar", concluida: true },
  { id: 2, titulo: "Codar", concluida: false },
];

const titulos = tarefas.map((tarefa) => tarefa.titulo);
const concluidas = tarefas.filter((tarefa) => tarefa.concluida);
const total = tarefas.reduce((acumulador) => acumulador + 1, 0);
```

Esses três métodos aparecem muito em:

* renderização de listas;
* filtragem de dados;
* transformação de resposta de API.

## Desestruturação

```javascript
const usuario = {
  nome: "Ana",
  cidade: "Passo Fundo",
};

const { nome, cidade } = usuario;
```

Também é comum em arrays:

```javascript
const cores = ["azul", "verde", "vermelho"];
const [primeiraCor, segundaCor] = cores;
```

## Modularização

Separar código em arquivos melhora muito a manutenção.

`math.js`

```javascript
export function add(a, b) {
  return a + b;
}
```

`main.js`

```javascript
import { add } from "./math.js";

console.log(add(2, 3));
```

## Relação com React Native

No aplicativo, essa mesma lógica será usada para:

* mapear listas em `FlatList`;
* separar componentes;
* organizar serviços;
* transformar dados de API antes de renderizar.

## Conclusão

Essa revisão fecha a ponte entre JavaScript puro e o desenvolvimento real do aplicativo. Os mesmos fundamentos continuam presentes, só passam a aparecer em componentes, telas e fluxos mais completos.
