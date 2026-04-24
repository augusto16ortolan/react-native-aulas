---
description: >-
  Executando tarefas em paralelo sem bloquear o fluxo do programa e manter a
  aplicação responsiva
---

# Assincronismo e o Javascript

<figure><img src="../.gitbook/assets/6.jpg" alt=""><figcaption></figcaption></figure>

Assincronidade é uma característica do Javascript que permite que certas operações sejam executadas no "fundo" enquanto o resto do código continua sendo executado. Isso é particularmente útil para operações que podem demorar um pouco para serem concluídas, como buscas de dados em servidores externos, leitura de arquivos, ou temporizadores.

### Conceitos básicos

* **Síncrono**: O código é executado linha por linha, uma após a outra. Se uma linha demorar muito tempo para ser executada, ela bloqueia a execução das linhas seguintes.
* **Assíncrono**: Permite que o código continue sendo executado sem precisar esperar que uma operação longa seja concluída. Quando a operação assíncrona é concluída, ela notifica o programa e executa uma função de retorno (callback).

### Exemplo explicativo

Vamos usar um exemplo simples com temporizadores para explicar.

#### Exemplo síncrono

Imagine que você está fazendo um bolo. Você mistura os ingredientes e espera 30 minutos até que o bolo esteja assado antes de fazer qualquer outra coisa.

```javascript
function fazerBolo() {
    console.log("Misturando ingredientes...");

    // Simula a espera de 30 minutos (não faça isso no seu código real!)
    let start = new Date().getTime();
    while (new Date().getTime() - start < 30000) {
        // espera 30 segundos
    }

    console.log("Bolo assado!");
}
```

No exemplo acima, o console.log("Fazendo outra coisa...") só será executado depois que o bolo estiver assado (após 30 segundos).

#### Exemplo assíncrono

Agora, imagine que você coloca o bolo no forno e enquanto ele assa, você faz outras coisas.

```javascript
function fazerBolo() {
    console.log("Misturando ingredientes...");

    // Usamos setTimeout para simular o tempo de espera de 30 segundos
    setTimeout(() => {
        console.log("Bolo assado!");
    }, 3000); // 3 segundos (em vez de 30 segundos para fins de demonstração)
}

fazerBolo();
console.log("Fazendo outra coisa enquanto o bolo assa..."); // Isso será executado imediatamente
```

Aqui, `setTimeout` é uma função assíncrona. Quando a função `fazerBolo` é chamada, ela coloca um temporizador para 3 segundos e continua a execução do código sem esperar. Assim, `console.log("Fazendo outra coisa enquanto o bolo assa...")` é executado imediatamente.

### Promises e Async/Await

Para tornar o código assíncrono mais legível, o JavaScript introduziu Promises e, mais tarde, `async/await`.

#### Promises

Uma Promise é um objeto usado para realizar processamentos assíncronos, esse objeto guarda um valor que pode estar disponível agora, no futuro ou nunca. Isso permite o tratamento de eventos ou ações que acontecem de forma assíncrona em casos de sucessos ou falhas.

Uma Promise também possuí diferentes estados, sendo alguns deles: Pendente (Pending), Resolvida (Resolved) (não está na documentação, mas gosto de definir esse estado também), Rejeitada (Rejected), Realizada (Fulfilled), Estabelecida (Settled). Geralmente os estados mais utilizados são dois (2), sendo eles: Resolvida e Rejeitada.

A Promise realiza processamentos e tratamentos de eventos ou ações assíncronas. Ao criar uma Promise, ela começa em estado inicial como pendente (pending), assim, os estados que ela pode ir são os demais informados anteriormente. Se ela estiver no estado de resolvida (resolved) é porque tudo deu certo, ou seja, a Promise foi criada e processada com sucesso, porém, em casos de falhas, ela estará no estado de rejeitada (rejected). Uma das maneiras de fazer esse tratamento é através das funções then e catch, para sucesso ou falha respectivamente (mais à frente será exemplificado e explicado).

```javascript
function assarBolo() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Bolo assado!");
        }, 3000);
    });
}

assarBolo().then(mensagem => {
    console.log(mensagem);
});

console.log("Fazendo outra coisa enquanto o bolo assa..."); // Isso será executado imediatamente
```

#### Async/Await

`async/await` é uma sintaxe mais simples e clara para trabalhar com Promises.

```javascript
function assarBolo() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve("Bolo assado!");
        }, 3000);
    });
}

async function fazerBolo() {
    console.log("Misturando ingredientes...");
    let mensagem = await assarBolo();
    console.log(mensagem);
}

fazerBolo();
console.log("Fazendo outra coisa enquanto o bolo assa..."); // Isso será executado imediatamente
```

### Conclusão

Assincronidade em Javascript permite que o código continue sendo executado sem esperar que certas operações sejam concluídas. Isso é essencial para criar aplicações rápidas e responsivas, especialmente quando se trabalha com operações que podem levar tempo, como requisições de rede ou leitura de arquivos.
