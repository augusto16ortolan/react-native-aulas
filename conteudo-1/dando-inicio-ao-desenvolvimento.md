---
description: >-
  Antes de entrar no React Native, vamos preparar a base de JavaScript e o
  ambiente que será usado ao longo do curso.
---

# Dando início ao desenvolvimento

<figure><img src="../.gitbook/assets/React Native (1).png" alt=""><figcaption></figcaption></figure>

Antes de escrever telas, consumir APIs e usar recursos do celular, precisamos alinhar a base do curso. Vamos trabalhar com:

* **JavaScript vanilla** para aprender lógica, sintaxe e organização do código;
* **Node.js** para usar ferramentas de desenvolvimento;
* **Expo** para criar e rodar nossos aplicativos React Native.

## JavaScript vanilla

Quando dizemos **vanilla JavaScript**, estamos falando do JavaScript puro, sem frameworks e sem abstrações extras em volta da linguagem.

Isso é importante por dois motivos:

1. você entende a linguagem de verdade;
2. quando chegar no React Native, o foco fica em aprender interface e arquitetura mobile, e não em “adivinhar” o que uma ferramenta faz por trás.

No começo do curso, essa escolha é intencional: aprender primeiro os fundamentos melhora muito a leitura e a manutenção dos projetos depois.

## O papel do Node.js

O **Node.js** permite executar JavaScript fora do navegador. No nosso contexto, ele é importante porque várias ferramentas do ecossistema dependem dele, como:

* `npm`;
* `npx`;
* `create-expo-app`;
* `expo`;
* `eas`.

Mesmo que o aplicativo rode no celular, grande parte do processo de desenvolvimento começa no terminal.

## Preparando o ambiente

Para acompanhar as aulas com tranquilidade, instale:

1. **Node.js LTS**
2. **Visual Studio Code**
3. **Git** (recomendado para versionamento)
4. **Expo Go** no celular, quando estivermos testando pelo app

Site oficial do Node.js: [https://nodejs.org/](https://nodejs.org/)

Depois da instalação, abra o terminal e confira:

```bash
node -v
npm -v
```

Se os dois comandos mostrarem uma versão, o ambiente básico está pronto.

## O que vem depois

Nesta primeira fase, vamos usar JavaScript puro para consolidar:

* tipos básicos;
* estruturas de decisão;
* laços de repetição;
* funções;
* arrays e objetos;
* assincronismo.

Essa base será reaproveitada o tempo todo no React Native, porque um aplicativo é, no fundo, uma combinação de:

* lógica em JavaScript;
* componentes React;
* recursos mobile;
* comunicação com APIs e serviços.

## Conclusão

O objetivo desta etapa não é “desviar” do desenvolvimento mobile, e sim criar uma fundação sólida para ele. Quando chegarmos nas telas, hooks, navegação e integração com backend, você vai perceber que quase tudo depende de uma boa leitura de JavaScript.
