---
description: >-
  Aprenda a configurar e otimizar seu ambiente de desenvolvimento para criar
  aplicativos de forma eficiente.
---

# Construção do ambiente de desenvolvimento

<figure><img src="../.gitbook/assets/React Native (5).png" alt=""><figcaption></figcaption></figure>

Agora que entendemos como funciona o desenvolvimento híbrido, vamos preparar o nosso ambiente para de fato começar a desenvolver aplicações em React Native.

Para nossas aulas, vamos utilizar o Expo, uma ferramenta que facilita a configuração e o desenvolvimento de aplicativos mais simples.

### Requisitos para o desenvolvimento com Expo

1. Node.js
2. Visual Studio Code
3. Dispositivo Android ou iOS
4. Aplicativo Expo Go instalado no seu dispositivo

Como descrito acima, vamos utilizar nossos próprios dispositivos para o desenvolvimento. Para isso, basta entrar na loja de aplicativo e baixar o app Expo Go.<br>

<figure><img src="../.gitbook/assets/image (16).png" alt="" width="128"><figcaption><p>Ícone do aplicativo Expo Go</p></figcaption></figure>

### Próximo passo

Para a criação do nosso projeto, vamos utilizar o comando a seguir:

```javascript
npx create-expo-app my-app-name --template
```

No lugar de "my-app-name" informe o nome do seu projeto.

O "--template" serve para podermos selecionar qual o modelo de desenvolvimento queremos utilizar, selecione o "Blank":

```javascript
? Choose a template: » - Use arrow-keys. Return to submit.
    Default
>   Blank - a minimal app as clean as an empty canvas
    Blank (TypeScript)
    Navigation (TypeScript)
    Blank (Bare)
```

Entre dentro da pasta do projeto gerado e siga o passo a baixo. Caso esteja utilizando Windows, pode usar o comando "cd my-app-name" para entrar na pasta do projeto.

Feito isso, o projeto será criado e podemos executar o seguinte comando para testarmos nosso app:

```
npm start
```

Ou também, pode ser executado o comando abaixo:

```
npx expo start
```

Pronto, projeto iniciado. Irá aparecer um QR Code no seu terminal, escaneie ele com o app Expo GO para poder ter acesso ao aplicativo.

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="498"><figcaption></figcaption></figure>

Feito isso, o app irá fazer o build e deve aparecer o seguinte no seu celular:

<figure><img src="../.gitbook/assets/Screenshot_20240726_140145_Expo Go.jpg" alt="" width="188"><figcaption></figcaption></figure>

Pronto, agora está tudo certo e podemos continuar nosso aprendizado com o desenvolvimento mobile.
