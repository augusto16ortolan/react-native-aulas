---
description: >-
  Aprenda a implementar navegação entre telas com React Navigation em projetos
  React Native com Expo.
---

# Navegação dentro do aplicativo

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

Poucos aplicativos funcionam com uma tela só. Em algum momento, o usuário precisa:

* abrir detalhes de um item;
* voltar para a página anterior;
* trocar de seção;
* acessar configurações;
* navegar por menus.

Para isso, vamos usar **React Navigation**, que continua sendo a principal biblioteca de navegação no ecossistema React Native.

## Instalando o React Navigation

Em um projeto Expo, a instalação base começa assim:

```bash
npm install @react-navigation/native
npx expo install react-native-screens react-native-safe-area-context
```

Depois, instalamos o navegador que queremos usar.

### Navegação em pilha com Native Stack

Para stack navigation, a escolha mais recomendada hoje é:

```bash
npm install @react-navigation/native-stack
```

### Navegação por abas

```bash
npm install @react-navigation/bottom-tabs
```

### Navegação com drawer

```bash
npm install @react-navigation/drawer
npx expo install react-native-gesture-handler react-native-reanimated
```

Sempre confirme dependências extras na documentação oficial do React Navigation:

[https://reactnavigation.org/docs/getting-started/](https://reactnavigation.org/docs/getting-started/)

## Navegação com stack

A navegação em pilha funciona como um histórico de telas: você entra em uma nova tela e pode voltar para a anterior.

### Exemplo de telas

`HomeScreen.js`

```jsx
import { View, Text, Button, StyleSheet } from "react-native";

export default function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Tela Inicial</Text>
      <Button
        title="Ir para detalhes"
        onPress={() =>
          navigation.navigate("Details", {
            itemId: 42,
            title: "Produto Exemplo",
          })
        }
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    padding: 20,
  },
  title: {
    fontSize: 24,
    fontWeight: "700",
    marginBottom: 12,
  },
});
```

`DetailsScreen.js`

```jsx
import { View, Text, Button, StyleSheet } from "react-native";

export default function DetailsScreen({ route, navigation }) {
  const { itemId, title } = route.params;

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Tela de Detalhes</Text>
      <Text>ID: {itemId}</Text>
      <Text>Título: {title}</Text>
      <Button title="Voltar" onPress={() => navigation.goBack()} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    padding: 20,
    gap: 12,
  },
  title: {
    fontSize: 24,
    fontWeight: "700",
  },
});
```

### Configurando o stack navigator

`App.js`

```jsx
import { NavigationContainer } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import HomeScreen from "./HomeScreen";
import DetailsScreen from "./DetailsScreen";

const Stack = createNativeStackNavigator();

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

## Navegação com tabs

Tabs servem para alternar entre seções principais do aplicativo.

```jsx
import { NavigationContainer } from "@react-navigation/native";
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";
import { View, Text } from "react-native";

function FeedScreen() {
  return (
    <View>
      <Text>Feed</Text>
    </View>
  );
}

function ProfileScreen() {
  return (
    <View>
      <Text>Perfil</Text>
    </View>
  );
}

const Tab = createBottomTabNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator>
        <Tab.Screen name="Feed" component={FeedScreen} />
        <Tab.Screen name="Perfil" component={ProfileScreen} />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

## Navegação com drawer

Drawer é útil quando o app precisa de um menu lateral com várias áreas.

```jsx
import { NavigationContainer } from "@react-navigation/native";
import { createDrawerNavigator } from "@react-navigation/drawer";
import { View, Text } from "react-native";

function HomeScreen() {
  return (
    <View>
      <Text>Home</Text>
    </View>
  );
}

function SettingsScreen() {
  return (
    <View>
      <Text>Configurações</Text>
    </View>
  );
}

const Drawer = createDrawerNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Drawer.Navigator>
        <Drawer.Screen name="Home" component={HomeScreen} />
        <Drawer.Screen name="Configurações" component={SettingsScreen} />
      </Drawer.Navigator>
    </NavigationContainer>
  );
}
```

## Passando dados entre telas

Uma das ações mais comuns em aplicativos é abrir uma tela de detalhes com informações da tela anterior.

### Enviando dados

```jsx
navigation.navigate("Details", {
  itemId: 42,
  title: "Produto Exemplo",
});
```

### Recebendo dados

```jsx
const { itemId, title } = route.params;
```

## Boas práticas para o curso

Ao estruturar projetos com navegação, tente separar assim:

* `screens/` para telas;
* `components/` para componentes reutilizáveis;
* `navigation/` para a configuração dos navegadores, se o projeto crescer.

## Conclusão

React Navigation continua sendo a escolha certa para o curso. O ponto principal não é decorar todos os navegadores, e sim entender a lógica: abrir telas, voltar, trocar de seção e passar dados entre rotas de forma clara.
