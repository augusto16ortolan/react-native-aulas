---
description: >-
  Aprenda a utilizar elementos essenciais para construir a interface e a
  funcionalidade do seu aplicativo.
---

# Componentes básicos do React Native

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Para começar a desenvolver com React Native, é essencial entender os componentes básicos que formam a estrutura de qualquer aplicativo. Estes componentes são os blocos de construção fundamentais que você usará para criar interfaces de usuário interativas e funcionais. Neste material, vamos explorar alguns dos componentes mais importantes do React Native, explicando seu uso e fornecendo exemplos práticos para ajudá-lo a começar.

## Guia dos componentes básicos do React Native

### View ([https://reactnative.dev/docs/view](https://reactnative.dev/docs/view))

O componente `View` é como uma "caixa" ou "contêiner" que pode conter outros componentes e organizá-los na tela.

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

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
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f0f0f0',
  },
});
```

### Text ([https://reactnative.dev/docs/text](https://reactnative.dev/docs/text))

O componente `Text` é usado para exibir texto na tela.

```jsx
import React from 'react';
import { Text } from 'react-native';

export default function App() {
  return (
    <Text>Este é um texto!</Text>
  );
}
```

### TextInput ([https://reactnative.dev/docs/textinput](https://reactnative.dev/docs/textinput))

O componente `TextInput` cria um campo de texto que captura entradas de texto do usuário.

```jsx
import React, { useState } from 'react';
import { TextInput } from 'react-native';

export default function App() {
  const [name, setName] = useState('');
  
  return (
    <TextInput placeholder="Digite seu nome" value={name} onChangeText={text => setName(text)}/>
    <Text>{name}</Text>
  );
}
```

### Button ([https://reactnative.dev/docs/button](https://reactnative.dev/docs/button))

O componente `Button` cria um botão clicável que pode executar uma ação quando pressionado.

```jsx
import React from 'react';
import { Button, Alert, View } from 'react-native';

export default function App() {
  return (
    <View>
      <Button
        title="Pressione-me"
        onPress={() => Alert.alert('Botão pressionado!')}
      />
    </View>
  );
}
```

### ScrollView ([https://reactnative.dev/docs/scrollview](https://reactnative.dev/docs/scrollview))

O componente `ScrollView` permite que o conteúdo dentro dele seja rolado, útil para listas ou layouts maiores que a tela.

```jsx
import React from 'react';
import { ScrollView, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <ScrollView style={styles.scrollView}>
      <Text>Item 1</Text>
      <Text>Item 2</Text>
      <Text>Item 3</Text>
      {/* Adicione mais itens conforme necessário */}
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  scrollView: {
    marginHorizontal: 20,
  },
});
```

### SafeAreaView ([https://reactnative.dev/docs/safeareaview](https://reactnative.dev/docs/safeareaview))

O componente `SafeAreaView` garante que o conteúdo seja exibido dentro das áreas seguras da tela, evitando a sobreposição com elementos do sistema, como a barra de status em dispositivos com "notch".

```jsx
import React from 'react';
import { SafeAreaView, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <SafeAreaView style={styles.safeArea}>
      <Text>Conteúdo seguro!</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
    backgroundColor: '#fff',
  },
});
```

### ActivityIndicator ([https://reactnative.dev/docs/activityindicator](https://reactnative.dev/docs/activityindicator))

O componente `ActivityIndicator` exibe um indicador de carregamento, útil para mostrar que uma operação está em andamento.

```jsx
import React from 'react';
import { ActivityIndicator, View, StyleSheet } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <ActivityIndicator size="large" color="#0000ff" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
});
```

### TouchableOpacity ([https://reactnative.dev/docs/touchableopacity](https://reactnative.dev/docs/touchableopacity))

O componente `TouchableOpacity` é usado para criar áreas tocáveis que respondem à interação do usuário com uma mudança de opacidade.

```jsx
import React from 'react';
import { TouchableOpacity, Text, StyleSheet, Alert } from 'react-native';

export default function App() {
  return (
    <TouchableOpacity style={styles.button} onPress={() => Alert.alert('Área tocada!')}>
      <Text style={styles.buttonText}>Toque aqui</Text>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: '#1E90FF',
    padding: 10,
    borderRadius: 5,
    alignItems: 'center',
  },
  buttonText: {
    color: '#fff',
    fontSize: 16,
  },
});
```

### StyleSheet ([https://reactnative.dev/docs/stylesheet](https://reactnative.dev/docs/stylesheet))

O `StyleSheet` é um método do React Native para criar estilos de forma organizada e eficiente.

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

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
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f8f8f8',
  },
  text: {
    fontSize: 18,
    color: '#333',
  },
});
```

### FlatList ([https://reactnative.dev/docs/flatlist](https://reactnative.dev/docs/flatlist))

Utilizado para renderizar grandes listas de dados de maneira eficiente.

```jsx
import React from 'react';
import { FlatList, Text, View } from 'react-native';

const DATA = [
  { id: '1', title: 'Item 1' },
  { id: '2', title: 'Item 2' },
  { id: '3', title: 'Item 3' },
];

export default function App() {
  return (
    <FlatList
      data={DATA}
      keyExtractor={(item) => item.id}
      renderItem={({ item }) => (
        <View>
          <Text>{item.title}</Text>
        </View>
      )}
    />
  );
}
```

### Image ([https://reactnative.dev/docs/image](https://reactnative.dev/docs/image))

Usado para exibir imagens.

```jsx
import React from 'react';
import { Image, View, StyleSheet } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Image
        style={styles.image}
        source={{ uri: 'https://reactnative.dev/img/tiny_logo.png' }}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  image: {
    width: 50,
    height: 50,
  },
});
```

Ao dominar esses componentes fundamentais, você estará bem preparado para enfrentar desafios mais avançados no desenvolvimento de aplicativos com React Native, aproveitando ao máximo a flexibilidade e o poder deste framework. Continue explorando, experimentando e construindo suas habilidades, e você verá como esses blocos de construção simples podem se transformar em aplicações completas e profissionais.
