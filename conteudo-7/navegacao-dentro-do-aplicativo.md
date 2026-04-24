---
description: >-
  Aprenda a implementar e gerenciar a navegação entre diferentes telas e seções
  do seu aplicativo, garantindo uma experiência de usuário fluida e intuitiva.
---

# Navegação dentro do aplicativo

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

Navegação é uma parte crucial de qualquer aplicativo móvel. Em React Native, o **React Navigation** é a biblioteca mais popular para gerenciar a navegação entre diferentes telas do aplicativo. Com ela, você pode criar uma navegação fluida usando diferentes tipos de navegação: Stack, Tabs e Drawer.

Vamos explorar cada tipo de navegação e aprender como passar dados de uma tela para outra.

### Instalando o React Navigation

Antes de começar, você precisa instalar o React Navigation e suas dependências. Primeiro vamos fazer a instalação apenas da Stack Navigation. No terminal, execute:

```javascript
npm install @react-navigation/native
npx expo install react-native-screens react-native-safe-area-context
npm install @react-navigation/stack
npx expo install react-native-gesture-handler @react-native-masked-view/masked-view
```

Lembrando que podemos seguir a documentação do React Navigation através desse link: [https://reactnavigation.org/docs/getting-started/](https://reactnavigation.org/docs/getting-started/)

### Navegação com Stack ([https://reactnavigation.org/docs/stack-navigator/](https://reactnavigation.org/docs/stack-navigator/))

A navegação em pilha (Stack Navigation) é como uma pilha de cartas. Quando você navega para uma nova tela, ela é empilhada sobre a tela anterior. Você pode voltar para a tela anterior puxando a carta de volta para baixo.

#### Exemplo de Stack Navigation

Crie uma tela de navegação (HomeScreen.js e DetailsScreen.js):

HomeScreen.js

```jsx
import React from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

export default function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text>Home Screen</Text>
      <Button
        title="Ir para Detalhes"
        onPress={() => navigation.navigate('Details', { itemId: 42 })}
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
});
```

DetailScreen.js

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function DetailsScreen({ route }) {
  const { itemId } = route.params;

  return (
    <View style={styles.container}>
      <Text>Detalhes da Tela</Text>
      <Text>ID do Item: {itemId}</Text>
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

Configure o Stack Navigator no App.js.

```jsx
import * as React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './HomeScreen';
import DetailsScreen from './DetailsScreen';

const Stack = createStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

### Navegação com Tabs ([https://reactnavigation.org/docs/tab-based-navigation/](https://reactnavigation.org/docs/tab-based-navigation/))

A navegação por abas (Tab Navigation) permite alternar entre diferentes telas usando abas na parte inferior da tela.

#### Exemplo de Tab Navigation

Crie telas de navegação (FeedScreen.js e ProfileScreen.js).

FeedScreen.js

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function FeedScreen() {
  return (
    <View style={styles.container}>
      <Text>Feed Screen</Text>
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

ProfileScreen.js

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function ProfileScreen() {
  return (
    <View style={styles.container}>
      <Text>Profile Screen</Text>
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

Configure o Tab Navigator no App.js.

```jsx
import * as React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import FeedScreen from './FeedScreen';
import ProfileScreen from './ProfileScreen';

const Tab = createBottomTabNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator>
        <Tab.Screen name="Feed" component={FeedScreen} />
        <Tab.Screen name="Profile" component={ProfileScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

### Navegação com Drawer ([https://reactnavigation.org/docs/drawer-based-navigation](https://reactnavigation.org/docs/drawer-based-navigation))

A navegação por gaveta (Drawer Navigation) permite que você deslize a partir da borda da tela para revelar um menu lateral com opções de navegação.

#### Exemplo de Drawer Navigation

Crie telas de navegação (HomeScreen.js, NotificationsScreen.js e SettingsScreen.js):

NotificationsScreen.js

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function NotificationsScreen() {
  return (
    <View style={styles.container}>
      <Text>Notifications Screen</Text>
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

SettingsScreen.js

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function SettingsScreen() {
  return (
    <View style={styles.container}>
      <Text>Settings Screen</Text>
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

Configure o Drawer Navigator no App.js:

```jsx
import * as React from 'react';
import { createDrawerNavigator } from '@react-navigation/drawer';
import { NavigationContainer } from '@react-navigation/native';
import HomeScreen from './HomeScreen';
import NotificationsScreen from './NotificationsScreen';
import SettingsScreen from './SettingsScreen';

const Drawer = createDrawerNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator initialRouteName="Home">
        <Drawer.Screen name="Home" component={HomeScreen} />
        <Drawer.Screen name="Notifications" component={NotificationsScreen} />
        <Drawer.Screen name="Settings" component={SettingsScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

### Passando dados de uma tela para outra

É comum precisar passar dados de uma tela para outra em um aplicativo. Veja como fazer isso com Stack Navigation.

#### Passar dados com navigation.navigate

Você pode passar dados para a próxima tela usando a função `navigation.navigate`. No exemplo abaixo, passamos um `itemId` para a tela de detalhes.

```jsx
// HomeScreen.js
<Button
  title="Ir para Detalhes"
  onPress={() => navigation.navigate('Details', { itemId: 42 })}
/>
```

#### Receber dados com route.params

Na tela de destino, você pode acessar os dados passados através da propriedade `route.params`.

```jsx
// DetailsScreen.js
export default function DetailsScreen({ route }) {
  const { itemId } = route.params;

  return (
    <View style={styles.container}>
      <Text>ID do Item: {itemId}</Text>
    </View>
  );
}
```

### Conclusão

A navegação é essencial para a experiência do usuário em aplicativos móveis. Com o React Navigation, você pode facilmente configurar diferentes tipos de navegação, como Stack, Tabs e Drawer. Cada tipo de navegação tem seus próprios usos e vantagens, e você pode escolher o que melhor se adapta às necessidades do seu aplicativo.

Passar dados entre telas também é uma tarefa comum e simples, utilizando as funcionalidades do React Navigation. Experimentar com diferentes tipos de navegação e como passar dados pode ajudar a criar uma navegação fluida e intuitiva em seu aplicativo.
