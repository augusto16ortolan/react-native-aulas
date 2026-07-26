---
description: >-
  Aprenda a utilizar componentes essenciais do React Native para montar a
  interface dos seus aplicativos.
---

# Componentes básicos do React Native

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Os componentes básicos do React Native são os blocos que usamos para montar telas, capturar dados do usuário, renderizar listas e exibir feedback visual.

Mais importante do que decorar todos os componentes é entender **quando** cada um deve ser usado.

## `View`

`View` é o contêiner mais comum do React Native. Ele agrupa elementos e ajuda a organizar o layout.

```jsx
import { View, Text, StyleSheet } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text>Olá, mundo!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#f0f0f0",
  },
});
```

## `Text`

`Text` é usado para exibir textos na tela.

```jsx
import { Text, View } from "react-native";

export default function App() {
  return (
    <View>
      <Text>Este é um texto!</Text>
    </View>
  );
}
```

## `TextInput`

`TextInput` captura texto digitado pelo usuário.

```jsx
import { useState } from "react";
import { TextInput, Text, View, StyleSheet } from "react-native";

export default function App() {
  const [name, setName] = useState("");

  return (
    <View style={styles.container}>
      <TextInput
        style={styles.input}
        placeholder="Digite seu nome"
        value={name}
        onChangeText={setName}
      />
      <Text>Olá, {name || "visitante"}!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    padding: 20,
  },
  input: {
    borderWidth: 1,
    borderColor: "#ccc",
    borderRadius: 8,
    paddingHorizontal: 12,
    paddingVertical: 10,
    marginBottom: 12,
  },
});
```

## `Button`

`Button` cria um botão simples com ação de toque.

```jsx
import { Alert, Button, View } from "react-native";

export default function App() {
  return (
    <View>
      <Button
        title="Pressione-me"
        onPress={() => Alert.alert("Ação", "Botão pressionado!")}
      />
    </View>
  );
}
```

Em projetos reais, muitas equipes preferem componentes próprios ou `Pressable`, porque `Button` tem pouca customização visual. Mesmo assim, ele é ótimo para aprender.

## `ScrollView`

`ScrollView` permite rolar conteúdo maior que a área visível da tela.

```jsx
import { ScrollView, Text, StyleSheet } from "react-native";

export default function App() {
  return (
    <ScrollView contentContainerStyle={styles.content}>
      <Text>Item 1</Text>
      <Text>Item 2</Text>
      <Text>Item 3</Text>
      <Text>Item 4</Text>
      <Text>Item 5</Text>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  content: {
    padding: 20,
    gap: 12,
  },
});
```

Para poucas informações, `ScrollView` funciona bem. Para listas grandes, prefira `FlatList`.

## `SafeAreaView` e área segura

Historicamente, o React Native trouxe o componente `SafeAreaView`, mas hoje a recomendação mais comum é usar a biblioteca **`react-native-safe-area-context`**.

Exemplo com `SafeAreaView` da biblioteca:

```jsx
import { SafeAreaView } from "react-native-safe-area-context";
import { Text, StyleSheet } from "react-native";

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <Text>Conteúdo dentro da área segura</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
  },
});
```

## `ActivityIndicator`

`ActivityIndicator` mostra que uma operação está em andamento.

```jsx
import { ActivityIndicator, View, StyleSheet } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <ActivityIndicator size="large" color="#1f3c88" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
});
```

## `TouchableOpacity` e `Pressable`

`TouchableOpacity` ainda aparece em muitos projetos, mas `Pressable` é uma opção mais moderna para várias interações.

Exemplo com `TouchableOpacity`:

```jsx
import { TouchableOpacity, Text, StyleSheet, Alert } from "react-native";

export default function App() {
  return (
    <TouchableOpacity
      style={styles.button}
      onPress={() => Alert.alert("Ação", "Área tocada!")}
    >
      <Text style={styles.buttonText}>Toque aqui</Text>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: "#1f3c88",
    padding: 14,
    borderRadius: 8,
    alignItems: "center",
  },
  buttonText: {
    color: "#fff",
    fontSize: 16,
    fontWeight: "600",
  },
});
```

## `StyleSheet`

`StyleSheet` organiza estilos e deixa o código mais legível.

```jsx
import { View, Text, StyleSheet } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Texto estilizado!</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 18,
    color: "#333",
  },
});
```

## `FlatList`

`FlatList` é a opção ideal para renderizar listas maiores com mais performance.

```jsx
import { FlatList, Text, View, StyleSheet } from "react-native";

const DATA = [
  { id: "1", title: "Item 1" },
  { id: "2", title: "Item 2" },
  { id: "3", title: "Item 3" },
];

export default function App() {
  return (
    <FlatList
      data={DATA}
      keyExtractor={(item) => item.id}
      contentContainerStyle={styles.list}
      renderItem={({ item }) => (
        <View style={styles.card}>
          <Text>{item.title}</Text>
        </View>
      )}
    />
  );
}

const styles = StyleSheet.create({
  list: {
    padding: 16,
    gap: 12,
  },
  card: {
    padding: 16,
    borderWidth: 1,
    borderColor: "#ddd",
    borderRadius: 8,
  },
});
```

## `Image`

`Image` exibe imagens locais ou remotas.

```jsx
import { Image, View, StyleSheet } from "react-native";

export default function App() {
  return (
    <View style={styles.container}>
      <Image
        style={styles.image}
        source={{ uri: "https://reactnative.dev/img/tiny_logo.png" }}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  image: {
    width: 60,
    height: 60,
  },
});
```

## Conclusão

Esses componentes aparecem o tempo todo em aplicativos reais. Aprender `View`, `Text`, `TextInput`, `FlatList`, `Image` e componentes de toque já permite construir boa parte de uma interface mobile funcional.
