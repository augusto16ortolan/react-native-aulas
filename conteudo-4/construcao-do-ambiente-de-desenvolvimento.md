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

Ao executar esse comando, o `create-expo-app` pode abrir um seletor de versão do SDK. Para as nossas aulas, a orientação é:

* escolher **For learning with Expo Go (SDK 54)**;
* manter o projeto em **JavaScript**;
* usar o template padrão, a menos que a atividade peça outro.

Isso é importante porque o **Expo Go** usado pela turma trabalha melhor nesse fluxo de aprendizado com **SDK 54**, reduzindo problemas de compatibilidade no começo do curso.

Depois da seleção, a ferramenta costuma seguir com uma mensagem parecida com:

```text
✔ Select an Expo SDK version: › For learning with Expo Go (SDK 54)
Creating meu-primeiro-app using the default template.
```

## E se eu quiser escolher um template?

Além do fluxo padrão, também é possível escolher explicitamente um template.

Exemplo:

```bash
npx create-expo-app@latest meu-primeiro-app --template blank
```

Esse formato é útil quando você quer começar com uma estrutura mais enxuta.

De forma prática para a disciplina:

* **fluxo principal da turma**: `npx create-expo-app@latest meu-primeiro-app`
* **seleção recomendada**: `SDK 54`
* **template padrão**: suficiente para a maioria das aulas
* **template `blank`**: opcional quando quisermos um projeto mais limpo

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
