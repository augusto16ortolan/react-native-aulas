# Context API

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

A Context API é uma funcionalidade do React que permite compartilhar valores entre componentes sem precisar passar props manualmente em cada nível da árvore de componentes. Isso é particularmente útil para gerenciar estados globais em sua aplicação, como temas, dados do usuário ou configurações.

No React Native, quando usamos Expo, o conceito e a implementação da Context API permanecem os mesmos que no React para a web. Vamos explorar como utilizá-la com um exemplo prático.

## O que é a Context API?

A Context API é uma forma de compartilhar dados que são considerados "globais" para uma árvore de componentes React. Ela evita o "prop drilling", que é o processo de passar dados através de múltiplos níveis de componentes.

### Componentes principais

1. **React.createContext**: Cria um novo contexto.
2. **Context.Provider**: Um componente que fornece o contexto para seus filhos.
3. **Context.Consumer**: Um componente que consome o contexto. No entanto, é mais comum utilizar o hook `useContext` para consumir o contexto.

### Exemplo prático

Vamos criar um exemplo simples onde usamos a Context API para gerenciar o estado de um tema (claro e escuro) em uma aplicação React Native com Expo.

#### Configuração do Projeto

Para usar a Context API dentro dos nossos aplicativos React Native, não é necessário nenhuma configuração adicional ou dependência externa, tudo está dentro da própria biblioteca do React.

#### Criar o contexto

Vamos criar um contexto para gerenciar o tema.

Crie um arquivo chamado `ThemeContext.js`:

```jsx
import React, { createContext, useState, useContext } from 'react';

// Cria o contexto
const ThemeContext = createContext();

// Componente Provider para envolver a aplicação
export const ThemeProvider = ({ children }) => {
  const [isDarkMode, setIsDarkMode] = useState(false);

  // Alterna entre modo claro e escuro
  const toggleTheme = () => {
    setIsDarkMode(!isDarkMode);
  };

  return (
    <ThemeContext.Provider value={{ isDarkMode, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

// Hook para consumir o contexto
export const useTheme = () => useContext(ThemeContext);
```

#### Integrar o Provider na aplicação

No arquivo `App.js`, vamos usar o `ThemeProvider` para envolver a árvore de componentes:

```jsx
import React from 'react';
import { SafeAreaView, Text, View, Button, StyleSheet } from 'react-native';
import { ThemeProvider, useTheme } from './ThemeContext';

const ThemedComponent = () => {
  const { isDarkMode, toggleTheme } = useTheme();

  return (
    <View style={styles.container}>
      <Text style={[styles.text, { color: isDarkMode ? 'white' : 'black' }]}>
        {isDarkMode ? 'Modo Escuro' : 'Modo Claro'}
      </Text>
      <Button title="Alternar Tema" onPress={toggleTheme} />
    </View>
  );
};

const App = () => {
  return (
    <ThemeProvider>
      <SafeAreaView style={styles.safeArea}>
        <ThemedComponent />
      </SafeAreaView>
    </ThemeProvider>
  );
};

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  container: {
    padding: 20,
    borderRadius: 10,
    backgroundColor: 'lightgrey',
    alignItems: 'center',
  },
  text: {
    fontSize: 18,
    marginBottom: 10,
  },
});

export default App;
```

* **`ThemeContext.js`**:
  * **`createContext`**: Cria um novo contexto chamado `ThemeContext`.
  * **`ThemeProvider`**: Componente que usa o `ThemeContext.Provider` para fornecer o estado e a função para alternar o tema.
  * **`useTheme`**: Hook personalizado para consumir o contexto de forma mais conveniente.
* **`App.js`**:
  * **`ThemedComponent`**: Componente que consome o contexto para exibir e alternar o tema. Usa o hook `useTheme` para acessar o estado `isDarkMode` e a função `toggleTheme`.
  * **`App`**: Componente principal que envolve a árvore de componentes com o `ThemeProvider`.

### Exemplo de controle de usuário com o Context API

Vamos criar uma aplicação onde temos um contexto de autenticação para gerenciar o estado de login do usuário. Os componentes poderão exibir informações do usuário e permitir que ele faça login e logout.

#### Criação do contexto de autenticação

Crie um arquivo chamado `AuthContext.js`:

```jsx
// AuthContext.js
import React, { createContext, useState, useContext } from 'react';

// Cria o contexto
const AuthContext = createContext();

// Componente Provider para envolver a aplicação
export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);

  // Função para realizar login
  const login = (username) => {
    setUser({ username });
  };

  // Função para realizar logout
  const logout = () => {
    setUser(null);
  };

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

// Hook para consumir o contexto
export const useAuth = () => useContext(AuthContext);
```

#### Criar componentes de Login e Perfil do Usuário

Crie um arquivo chamado `AuthScreens.js`:

```jsx
import React, { useState } from 'react';
import { View, Text, Button, TextInput, StyleSheet } from 'react-native';
import { useAuth } from './AuthContext';

// Componente de Login
export const LoginScreen = () => {
  const [username, setUsername] = useState('');
  const { login } = useAuth();

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Login</Text>
      <TextInput
        style={styles.input}
        placeholder="Digite seu nome de usuário"
        value={username}
        onChangeText={setUsername}
      />
      <Button title="Entrar" onPress={() => login(username)} />
    </View>
  );
};

// Componente de Perfil
export const ProfileScreen = () => {
  const { user, logout } = useAuth();

  if (!user) {
    return <Text style={styles.message}>Você não está logado.</Text>;
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Bem-vindo, {user.username}!</Text>
      <Button title="Sair" onPress={logout} />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
  },
  title: {
    fontSize: 24,
    marginBottom: 20,
  },
  input: {
    height: 40,
    borderColor: 'gray',
    borderWidth: 1,
    width: '100%',
    paddingHorizontal: 10,
    marginBottom: 20,
  },
  message: {
    fontSize: 18,
  },
});
```

#### Integrar o contexto e componentes na aplicação

Modifique o `App.js` para usar o `AuthProvider` e renderizar os componentes `LoginScreen` e `ProfileScreen` com base no estado de autenticação:

```jsx
import React from 'react';
import { SafeAreaView, StyleSheet } from 'react-native';
import { AuthProvider } from './AuthContext';
import { LoginScreen, ProfileScreen } from './AuthScreens';

// Componente principal da aplicação
const App = () => {
  return (
    <AuthProvider>
      <SafeAreaView style={styles.safeArea}>
        <ProfileScreen />
        {/* Use o componente LoginScreen para testar a funcionalidade */}
        {/* <LoginScreen /> */}
      </SafeAreaView>
    </AuthProvider>
  );
};

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
  },
});

export default App;
```

* **`AuthContext.js`**:
  * **`createContext`**: Cria um novo contexto chamado `AuthContext` para autenticação de usuários.
  * **`AuthProvider`**: Componente que fornece o estado global do usuário e as funções `login` e `logout` através do `AuthContext.Provider`.
  * **`useAuth`**: Hook personalizado para consumir o contexto de autenticação.
* **`AuthScreens.js`**:
  * **`LoginScreen`**: Componente que permite ao usuário fazer login. Usa o hook `useAuth` para chamar a função `login` quando o botão é pressionado.
  * **`ProfileScreen`**: Componente que exibe informações do usuário autenticado e um botão para sair. Usa o hook `useAuth` para obter o estado do usuário e chamar a função `logout`.
* **`App.js`**:
  * **`AuthProvider`**: Envolvemos a árvore de componentes com o `AuthProvider` para fornecer o contexto de autenticação.
  * **`ProfileScreen`**: Exibe o perfil do usuário se estiver autenticado. Você pode alternar para `LoginScreen` para testar o login.

## Conclusão

Neste exemplo, aprendemos como criar e usar a Context API em uma aplicação React Native com Expo. A Context API simplifica a passagem de dados através dos componentes e ajuda a manter o código mais limpo e organizado.
