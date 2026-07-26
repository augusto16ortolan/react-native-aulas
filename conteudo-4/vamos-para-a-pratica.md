---
description: >-
  Nesta seção, vamos conhecer a estrutura inicial de um projeto Expo em
  JavaScript e modificar o primeiro app.
---

# Vamos para a prática?

<figure><img src="../.gitbook/assets/165238eb-4601-4aae-b8ad-6dc322811aca_text.gif" alt=""><figcaption></figcaption></figure>

Com o projeto criado e rodando, o próximo passo é entender o arquivo inicial do aplicativo.

Antes de seguir, vale reforçar o padrão da disciplina:

* criar o projeto com `npx create-expo-app@latest`;
* escolher **SDK 54** no seletor, pensando no uso com **Expo Go**;
* manter o projeto em **JavaScript**;
* usar o template padrão ou, quando o professor pedir, o `blank`.

## Documentações importantes

Durante o curso, estas duas documentações serão referências frequentes:

{% embed url="https://reactnative.dev/docs/components-and-apis" %}

{% embed url="https://docs.expo.dev/" %}

## Um exemplo inicial de `App.js`

Um projeto Expo em JavaScript costuma começar com uma estrutura parecida com esta:

```jsx
import { StatusBar } from "expo-status-bar";
import { StyleSheet, Text, View } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

## O que esse código faz

### Importações

```javascript
import { StatusBar } from "expo-status-bar";
import { StyleSheet, Text, View } from "react-native";
```

Aqui estamos trazendo:

* `StatusBar`: controla a aparência da barra de status;
* `View`: funciona como um contêiner;
* `Text`: mostra texto na tela;
* `StyleSheet`: organiza os estilos.

### Componente principal

```jsx
export default function App() {
  return (
    <View style={styles.container}>
      <Text>Open up App.js to start working on your app!</Text>
      <StatusBar style="auto" />
    </View>
  );
}
```

Esse componente é a primeira tela do app. Tudo o que renderizarmos aqui será exibido quando o aplicativo abrir.

### Estilos

```jsx
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
  },
});
```

Esses estilos deixam o conteúdo centralizado na tela.

## Primeira modificação prática

Vamos trocar o texto inicial e personalizar um pouco a interface:

```jsx
import { StatusBar } from "expo-status-bar";
import { StyleSheet, Text, View } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Projeto de Desenvolvimento de Aplicativos</Text>
      <Text style={styles.subtitle}>Primeiro app com React Native e Expo</Text>
      <StatusBar style="light" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#1f3c88",
    alignItems: "center",
    justifyContent: "center",
    padding: 24,
  },
  title: {
    color: "#fff",
    fontSize: 24,
    fontWeight: "700",
    textAlign: "center",
    marginBottom: 12,
  },
  subtitle: {
    color: "#dbe4ff",
    fontSize: 16,
    textAlign: "center",
  },
});
```

## O que mudamos

* alteramos a cor de fundo;
* estilizamos o texto;
* adicionamos uma segunda linha de informação;
* ajustamos a barra de status para combinar com o fundo.

## Leitura importante sobre estilos

No React Native, o estilo lembra CSS em vários pontos, mas não é CSS puro. Algumas propriedades são parecidas, outras mudam, e a forma de declarar tudo é em objetos JavaScript.

Isso significa que:

* nomes como `backgroundColor` e `fontSize` usam `camelCase`;
* os valores são escritos dentro de objetos;
* os estilos ficam muito próximos da lógica do componente.

## Conclusão

Esse primeiro contato com o `App.js` já mostra a ideia central do React Native: criar interfaces a partir de componentes e estilos em JavaScript. A partir daqui, vamos expandir esse mesmo princípio para inputs, listas, navegação e integração com dados.
