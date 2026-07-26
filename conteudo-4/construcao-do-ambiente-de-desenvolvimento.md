---
description: >-
  Aprenda a preparar o ambiente de desenvolvimento com Expo para criar
  aplicativos React Native em JavaScript.
---

# Construção do ambiente de desenvolvimento

<figure><img src="../.gitbook/assets/React Native (5).png" alt=""><figcaption></figcaption></figure>

Agora vamos sair da teoria e preparar o ambiente que será usado no restante do curso.

Nossa decisão aqui é intencional:

* **React Native com Expo**
* **JavaScript vanilla**
* **testes rápidos no celular e no emulador, quando necessário**

## O que você precisa instalar

1. **Node.js LTS**
2. **Visual Studio Code**
3. **Expo Go** no celular Android ou iPhone

Se quiser um fluxo mais completo, também vale ter:

* **Git**
* **Android Studio** para emulador Android
* **Xcode** no macOS para simulador iOS

## Criando um projeto Expo em JavaScript

O fluxo atual recomendado para criar um projeto é com `create-expo-app`.

No terminal, execute:

```bash
npx create-expo-app@latest meu-primeiro-app
```

Se a ferramenta abrir um seletor de template, escolha uma opção em **JavaScript**. Se existir uma versão “blank” ou “default” em JavaScript, ela é suficiente para o curso.

Depois entre na pasta do projeto:

```bash
cd meu-primeiro-app
```

## Rodando o projeto

Para iniciar o ambiente local:

```bash
npx expo start
```

Você também pode usar:

```bash
npm start
```

Os dois caminhos funcionam, mas ao longo do curso vamos preferir `npx expo start`, porque ele deixa mais explícito que estamos usando a ferramenta do Expo.

## Testando no celular com Expo Go

Com o servidor iniciado, o terminal exibirá um QR Code.

Faça assim:

1. abra o **Expo Go** no celular;
2. escaneie o QR Code;
3. aguarde o carregamento do projeto.

Esse fluxo é muito útil no começo porque elimina boa parte da configuração nativa e permite validar as telas rapidamente.

## Estrutura inicial esperada

Dependendo do template escolhido, você pode encontrar diferenças pequenas na estrutura. Em geral, os pontos importantes são:

* um arquivo principal como `App.js`;
* `package.json` com os scripts do projeto;
* dependências do Expo e React Native já configuradas.

No nosso curso, o importante é entender que **`App.js` será o ponto de entrada inicial do aplicativo**.

## Boas práticas desde o começo

Antes de continuar, vale criar alguns hábitos:

* manter o projeto em uma pasta com nome simples;
* evitar espaços e acentos no nome da pasta;
* rodar o app antes de instalar várias bibliotecas;
* confirmar que o ambiente está funcionando antes de começar a codar.

## Conclusão

Com esse ambiente pronto, você já tem o necessário para acompanhar as aulas e desenvolver aplicações mobile em React Native com JavaScript. A partir daqui, nosso foco deixa de ser configuração e passa a ser construção de interface, lógica e integração.
