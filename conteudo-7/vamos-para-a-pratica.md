# Vamos para a prática?

<figure><img src="../.gitbook/assets/165238eb-4601-4aae-b8ad-6dc322811aca_text.gif" alt=""><figcaption></figcaption></figure>

Nesta prática, vamos montar uma navegação simples usando **React Navigation** com **Native Stack**, que é uma ótima opção para começar.

## Estrutura sugerida

```text
src/
  screens/
    HomeScreen.js
    DetailsScreen.js
App.js
```

## Criando as telas

### `src/screens/HomeScreen.js`

```jsx
import { View, Text, Button, StyleSheet } from "react-native";

export default function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Tela Inicial</Text>
      <Button
        title="Ver detalhes do curso"
        onPress={() =>
          navigation.navigate("Details", {
            course: "React Native",
            module: "Navegação",
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
    marginBottom: 16,
  },
});
```

### `src/screens/DetailsScreen.js`

```jsx
import { View, Text, Button, StyleSheet } from "react-native";

export default function DetailsScreen({ navigation, route }) {
  const { course, module } = route.params;

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Tela de Detalhes</Text>
      <Text>Curso: {course}</Text>
      <Text>Módulo: {module}</Text>
      <Button title="Voltar para Home" onPress={() => navigation.goBack()} />
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

## Configurando o navegador

### `App.js`

```jsx
import { NavigationContainer } from "@react-navigation/native";
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import HomeScreen from "./src/screens/HomeScreen";
import DetailsScreen from "./src/screens/DetailsScreen";

const Stack = createNativeStackNavigator();

export default function App() {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen
          name="Home"
          component={HomeScreen}
          options={{ title: "Início" }}
        />
        <Stack.Screen
          name="Details"
          component={DetailsScreen}
          options={{ title: "Detalhes" }}
        />
      </Stack.Navigator>
    </NavigationContainer>
  );
}
```

## O que cada parte faz

### `NavigationContainer`

É o componente que envolve toda a árvore de navegação e permite que o React Navigation controle o estado das rotas.

### `createNativeStackNavigator`

Cria o navegador de pilha usando componentes nativos, o que tende a oferecer uma experiência visual melhor e mais próxima do sistema operacional.

### `Stack.Navigator`

Define o conjunto de telas que fazem parte da pilha de navegação.

### `Stack.Screen`

Representa cada tela disponível nessa pilha.

## O que praticar depois

Quando esse exemplo estiver funcionando, experimente:

1. mudar os títulos das telas;
2. adicionar mais parâmetros no `navigate`;
3. criar uma terceira tela;
4. definir uma tela inicial diferente;
5. personalizar o cabeçalho com `options`.

## Conclusão

Com esse exemplo, você já monta a base de navegação de muitos aplicativos. A partir daqui, o próximo passo é combinar navegação com listas, formulários, autenticação e consumo de APIs.
