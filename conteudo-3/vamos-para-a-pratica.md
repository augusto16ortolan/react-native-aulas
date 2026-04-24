---
description: >-
  Nessa prática, vamos integrar todos os conceitos já vistos nos conteúdos,
  desde o mais básico ao mais avançado deles.
---

# Vamos para a prática?

<div data-full-width="true"><figure><img src="../.gitbook/assets/165238eb-4601-4aae-b8ad-6dc322811aca_text.gif" alt=""><figcaption></figcaption></figure></div>

Agora vamos montar um código que integre todos os conceitos mencionados em uma aplicação simples de lista de tarefas, uma Todo List. O código incluíra conceitos como: console.log para imprimir no terminal, as estruturas de controle if, else if e else, loops como while e for, funções, arrays e os métodos filter e map.

Para começar, vamos estruturar nosso projeto em dois arquivos, para podermos ver como a modularização funciona.

* **`tasks.js`**: Contém funções relacionadas à manipulação de tarefas.
* **`main.js`**: Arquivo principal que importa e utiliza as funções do módulo de tarefas.

#### tasks.js

```javascript
// Função para adicionar uma tarefa
export const adicionarTarefa = (lista, tarefa) => {
    lista.push({ tarefa, completa: false });
};

// Função para listar todas as tarefas
export const listarTarefas = (lista) => {
    console.log("Lista de Tarefas:");
    lista.forEach((item, index) => {
        console.log(`${index + 1}. ${item.tarefa} - ${item.completa ? 'Completa' : 'Pendente'}`);
    });
};

// Função para marcar uma tarefa como completa
export const completarTarefa = (lista, index) => {
    if (index >= 0 && index < lista.length) {
        lista[index].completa = true;
    } else {
        console.log("Índice inválido.");
    }
};

// Função para filtrar tarefas completas
export const filtrarTarefasCompletas = (lista) => {
    return lista.filter(item => item.completa);
};

// Função para mapear tarefas para um formato de string
export const mapearTarefasParaString = (lista) => {
    return lista.map(item => `${item.tarefa} - ${item.completa ? 'Completa' : 'Pendente'}`);
};
```

Este código contém um conjunto de funções para gerenciar uma lista de tarefas. A função `adicionarTarefa` adiciona uma nova tarefa à lista com um status inicial de "não completa". A função `listarTarefas` exibe todas as tarefas, mostrando se cada uma está completa ou pendente. A função `completarTarefa` marca uma tarefa específica como completa com base no índice fornecido. A função `filtrarTarefasCompletas` retorna apenas as tarefas que estão completas. Por fim, a função `mapearTarefasParaString` transforma a lista de tarefas em uma lista de strings formatadas, indicando o status de cada tarefa.

#### main.js

```javascript
import { adicionarTarefa, listarTarefas, completarTarefa, filtrarTarefasCompletas, mapearTarefasParaString } from './tasks.js';

const main = () => {
    let listaDeTarefas = [];

    // Adicionando tarefas
    adicionarTarefa(listaDeTarefas, "Estudar JavaScript");
    adicionarTarefa(listaDeTarefas, "Fazer exercícios");
    adicionarTarefa(listaDeTarefas, "Ler um livro");

    // Listando todas as tarefas
    listarTarefas(listaDeTarefas);

    // Marcando a segunda tarefa como completa
    completarTarefa(listaDeTarefas, 1);

    // Listando todas as tarefas novamente para ver a mudança
    console.log("\nApós completar uma tarefa:");
    listarTarefas(listaDeTarefas);

    // Filtrando e listando apenas as tarefas completas
    console.log("\nTarefas Completas:");
    const tarefasCompletas = filtrarTarefasCompletas(listaDeTarefas);
    listarTarefas(tarefasCompletas);

    // Mapeando tarefas para string e listando
    console.log("\nTarefas em Formato de String:");
    const tarefasEmString = mapearTarefasParaString(listaDeTarefas);
    tarefasEmString.forEach(tarefa => console.log(tarefa));
};

// Executando a função principal
main();
```

Este código define e executa uma função principal (`main`) para gerenciar uma lista de tarefas usando as funções importadas do módulo `tasks.js`. Inicialmente, ele cria uma lista vazia de tarefas. Em seguida, adiciona três tarefas à lista e as lista todas. A segunda tarefa é marcada como completa, e a lista é exibida novamente para refletir essa mudança. Depois, o código filtra e exibe apenas as tarefas completas. Finalmente, ele converte a lista de tarefas para um formato de string e imprime cada uma delas. Essa abordagem demonstra a aplicação prática dos conceitos de manipulação de arrays e funções modularizadas.

### Conclusão

Neste exemplo, usamos modularização para separar a lógica de manipulação de tarefas em um arquivo (`tasks.js`) e a lógica principal em outro (`main.js`). Essa abordagem torna o código mais organizado, fácil de manter e reutilizável.
