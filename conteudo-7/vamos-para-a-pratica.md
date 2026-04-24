# Vamos para a prática?

<figure><img src="../.gitbook/assets/165238eb-4601-4aae-b8ad-6dc322811aca_text.gif" alt=""><figcaption></figcaption></figure>

Nesta prática, vamos aprender a usar o `Stack.Navigator` para gerenciar a navegação entre diferentes telas de um aplicativo React Native. Vamos construir um exemplo básico onde temos duas telas e podemos navegar de uma para a outra.

### Configuração do Navegador de Pilha (Stack Navigator)

Agora vamos configurar o Stack Navigator.

#### Criação das telas

Vamos criar duas telas simples. No diretório `screens`, crie dois arquivos: `HomeScreen.js` e `DetailsScreen.js`.

```jsx
import React from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

const HomeScreen = ({ navigation }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Tela Inicial</Text>
      <Button
        title="Ir para Detalhes"
        onPress={() => navigation.navigate('Details')}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    fontSize: 24,
  },
});

export default HomeScreen;
```

```jsx
import React from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

const DetailsScreen = ({ navigation }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Tela de Detalhes</Text>
      <Button
        title="Voltar para Home"
        onPress={() => navigation.goBack()}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    fontSize: 24,
  },
});

export default DetailsScreen;
```

No arquivo App.js, temos o seguinte conteúdo:

```jsx
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import HomeScreen from './screens/HomeScreen';
import DetailsScreen from './screens/DetailsScreen';

const Stack = createStackNavigator();

const App = () => {
  return (
    <NavigationContainer>
      <Stack.Navigator initialRouteName="Home">
        <Stack.Screen name="Home" component={HomeScreen} />
        <Stack.Screen name="Details" component={DetailsScreen} />
      </Stack.Navigator>
    </NavigationContainer>
  );
};

export default App;
```

Aqui está o que cada parte do código faz:

**a) NavigationContainer**

**O que é?** O `NavigationContainer` é um componente de nível superior que deve envolver toda a árvore de navegação do seu aplicativo. Ele fornece o contexto de navegação necessário para que o React Navigation funcione corretamente.

**Por que é necessário?** O `NavigationContainer` gerencia o estado da navegação e o histórico de navegação. Sem ele, o React Navigation não terá um contexto para trabalhar, e a navegação entre telas não funcionará.

**Onde você usa?** Você deve envolver o seu `Stack.Navigator` (ou qualquer outro tipo de navegador) com o `NavigationContainer`. Normalmente, isso é feito no componente raiz do seu aplicativo.



**b) createStackNavigator**

**O que é?** A função `createStackNavigator` cria um objeto que contém a lógica e os componentes necessários para implementar a navegação em pilha (stack navigation). Em outras palavras, ele cria um "navegador de pilha" que gerencia a navegação entre telas de forma empilhada.

**Por que é necessário?** O `createStackNavigator` é necessário para configurar e criar um "navegador de pilha" que gerencia a transição entre diferentes telas (ou rotas) dentro do seu aplicativo. Ele permite que você defina quais telas estarão disponíveis na pilha e como elas serão exibidas.

**Onde você usa?** Você usa `createStackNavigator` para criar uma instância do Stack Navigator e depois usa essa instância para definir as telas do seu aplicativo.



**c) Stack.Navigator**

**O que é?** O `Stack.Navigator` é um componente que atua como um container para as telas que você deseja exibir. Ele define a pilha de navegação e controla como as telas são empilhadas e desenroladas.

**Por que é necessário?** O `Stack.Navigator` gerencia a navegação entre as telas dentro de uma pilha. Ele determina qual tela está no topo da pilha e lida com as transições entre as telas quando você navega para frente ou para trás.

**Onde você usa?** Você usa o `Stack.Navigator` para definir quais telas estão na pilha e configurar opções de navegação, como cabeçalhos, animações e outras configurações.



**d) Stack.Screen**

**O que é?** O `Stack.Screen` é um componente filho do `Stack.Navigator` que define uma tela individual na pilha de navegação. Cada `Stack.Screen` representa uma tela específica do seu aplicativo.

**Por que é necessário?** Cada `Stack.Screen` diz ao Stack Navigator quais componentes (telas) devem ser exibidos em cada parte da pilha de navegação. Você define o nome da tela e o componente que deve ser exibido quando essa tela estiver ativa.

**Onde você usa?** Você usa o `Stack.Screen` dentro do `Stack.Navigator` para definir todas as telas disponíveis na navegação.



Com esses conceitos claros, você pode configurar a navegação entre telas em seu aplicativo React Native usando o React Navigation. Se precisar de mais detalhes ou de exemplos avançados, é só me avisar!
