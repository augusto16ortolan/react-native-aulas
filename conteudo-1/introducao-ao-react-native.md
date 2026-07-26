---
description: Explorando o desenvolvimento de aplicativos com React Native e Expo
---

# Introdução ao React Native

<figure><img src="../.gitbook/assets/React Native.png" alt=""><figcaption></figcaption></figure>

O **React Native** é uma tecnologia usada para desenvolver aplicativos móveis com **JavaScript** e **React**, permitindo criar apps para Android e iOS a partir de uma base de código compartilhada.

Neste curso, vamos trabalhar com **JavaScript vanilla** como linguagem-base. A ideia é aprender a lógica e os conceitos do desenvolvimento mobile sem aumentar a dificuldade logo no início com tipagem estática. Isso não diminui a qualidade do projeto: muitos aplicativos reais começaram em JavaScript e evoluíram com o tempo.

## React Native e desenvolvimento multiplataforma

Quando falamos em desenvolvimento mobile, existem três caminhos bastante comuns:

* **Nativo**: um código para Android e outro para iOS.
* **Multiplataforma**: uma base de código compartilhada para mais de uma plataforma.
* **Híbrido baseado em WebView**: interface construída com tecnologias web dentro de um contêiner.

O React Native fica no grupo de tecnologias **multiplataforma**, mas com uma diferença importante: ele não renderiza a interface como uma página web dentro de um navegador embutido. Em vez disso, ele trabalha com **componentes nativos** da plataforma.

Isso faz com que a experiência visual e o comportamento do aplicativo fiquem muito mais próximos de um app nativo.

## Por que usar React Native?

Alguns motivos tornam o React Native uma escolha forte para aprender e construir projetos:

* **Código compartilhado**: grande parte da lógica e da interface pode ser reutilizada entre Android e iOS.
* **Ecossistema sólido**: existe uma comunidade muito grande, com bibliotecas maduras para navegação, formulários, autenticação, câmera, mapas e muito mais.
* **Integração com recursos do celular**: câmera, armazenamento, notificações, localização e outros recursos podem ser acessados com bibliotecas do ecossistema.
* **Ciclo de desenvolvimento rápido**: durante o desenvolvimento, é possível testar mudanças rapidamente no emulador ou no celular.

## O papel do Expo no curso

Neste material, vamos usar o **Expo**, que é uma plataforma e um conjunto de ferramentas em torno do React Native.

Com o Expo, conseguimos:

* criar projetos com menos configuração inicial;
* rodar o app com mais facilidade;
* acessar várias APIs do dispositivo com bibliotecas prontas;
* gerar builds para teste e publicação com um fluxo mais simples.

Para o nosso objetivo didático, Expo + React Native + JavaScript é uma combinação excelente: reduz a complexidade inicial e mantém o foco no que realmente importa, que é aprender a construir aplicativos.

## Ecossistema que vamos usar

Ao longo do curso, você vai encontrar com frequência estas peças do ecossistema:

1. **Expo**
   * criação do projeto;
   * execução local;
   * bibliotecas oficiais para recursos mobile;
   * geração de builds com EAS.
2. **React Navigation**
   * navegação entre telas;
   * stacks, tabs e drawer;
   * passagem de parâmetros.
3. **Axios e Fetch**
   * consumo de APIs;
   * envio e recebimento de dados.
4. **Context API**
   * compartilhamento de estado entre componentes.
5. **Supabase**
   * autenticação;
   * banco de dados;
   * storage para arquivos.

## Mercado e relevância

O React Native continua relevante em produtos reais, especialmente em equipes que precisam:

* lançar Android e iOS com menos tempo;
* validar um MVP rapidamente;
* compartilhar lógica entre plataformas;
* manter um time menor sem abrir mão de uma boa experiência.

Mais importante do que decorar nomes de bibliotecas é entender o fluxo: **interface, estado, navegação, dados e publicação**. É isso que faz alguém sair do “estou vendo tutorial” para “consigo construir um aplicativo funcional”.

## Conclusão

Neste curso, vamos usar o React Native como base para aprender o desenvolvimento de aplicativos modernos, com foco em **JavaScript**, **Expo** e boas práticas reais de projeto. O objetivo não é apenas montar telas, mas entender como um app nasce, cresce, consome dados, navega entre páginas e fica pronto para ser testado e publicado.
