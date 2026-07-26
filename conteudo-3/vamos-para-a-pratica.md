---
description: >-
  Vamos integrar os conceitos de JavaScript com um pequeno exemplo modular de
  lista de tarefas.
---

# Vamos para a prática?

<figure><img src="../.gitbook/assets/165238eb-4601-4aae-b8ad-6dc322811aca_text.gif" alt=""><figcaption></figcaption></figure>

Vamos usar dois arquivos para mostrar modularização e manipulação de arrays.

## `tasks.js`

```javascript
export function adicionarTarefa(lista, tarefa) {
  lista.push({ tarefa, completa: false });
}

export function completarTarefa(lista, index) {
  if (index >= 0 && index < lista.length) {
    lista[index].completa = true;
  }
}

export function filtrarTarefasCompletas(lista) {
  return lista.filter((item) => item.completa);
}
```

## `main.js`

```javascript
import {
  adicionarTarefa,
  completarTarefa,
  filtrarTarefasCompletas,
} from "./tasks.js";

const listaDeTarefas = [];

adicionarTarefa(listaDeTarefas, "Estudar JavaScript");
adicionarTarefa(listaDeTarefas, "Aprender React Native");
completarTarefa(listaDeTarefas, 1);

console.log(listaDeTarefas);
console.log(filtrarTarefasCompletas(listaDeTarefas));
```

## Conclusão

Mesmo sendo simples, esse padrão já prepara o aluno para a estrutura que será usada em componentes, serviços e telas do app.
