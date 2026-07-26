# Context API

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

A **Context API** é um recurso do React usado para compartilhar valores entre componentes sem precisar passar props manualmente por vários níveis.

Ela é útil quando um dado precisa ser acessado em muitos lugares da aplicação, como:

* tema;
* usuário autenticado;
* idioma;
* carrinho;
* configurações globais.

## Quando faz sentido usar Context

Use Context quando o valor:

* é global ou quase global;
* será consumido por várias telas ou componentes;
* ficaria incômodo de passar por props manualmente.

Se o dado é local de uma única tela, normalmente `useState` já resolve.

## Exemplo 1: tema global

### `ThemeContext.js`

```jsx
import { createContext, useContext, useState } from "react";

const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("light");

  function toggleTheme() {
    setTheme((currentTheme) =>
      currentTheme === "light" ? "dark" : "light"
    );
  }

  return (
    <ThemeContext.Provider value={{ theme, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export function useTheme() {
  return useContext(ThemeContext);
}
```

### `App.js`

```jsx
import { View, Text, Button, StyleSheet } from "react-native";
import { ThemeProvider, useTheme } from "./ThemeContext";

function HomeScreen() {
  const { theme, toggleTheme } = useTheme();
  const isDark = theme === "dark";

  return (
    <View
      style={[
        styles.container,
        { backgroundColor: isDark ? "#111827" : "#f9fafb" },
      ]}
    >
      <Text style={{ color: isDark ? "#fff" : "#111", marginBottom: 12 }}>
        Tema atual: {theme}
      </Text>
      <Button title="Alternar tema" onPress={toggleTheme} />
    </View>
  );
}

export default function App() {
  return (
    <ThemeProvider>
      <HomeScreen />
    </ThemeProvider>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    padding: 20,
  },
});
```

## Exemplo 2: autenticação simples

### `AuthContext.js`

```jsx
import { createContext, useContext, useState } from "react";

const AuthContext = createContext();

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  function login(username) {
    setUser({ username });
  }

  function logout() {
    setUser(null);
  }

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
}

export function useAuth() {
  return useContext(AuthContext);
}
```

### `AuthScreens.js`

```jsx
import { useState } from "react";
import { View, Text, Button, TextInput, StyleSheet } from "react-native";
import { useAuth } from "./AuthContext";

export function LoginScreen() {
  const [username, setUsername] = useState("");
  const { login } = useAuth();

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Login</Text>
      <TextInput
        style={styles.input}
        placeholder="Digite seu nome"
        value={username}
        onChangeText={setUsername}
      />
      <Button title="Entrar" onPress={() => login(username)} />
    </View>
  );
}

export function ProfileScreen() {
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
    marginBottom: 20,
  },
  input: {
    width: "100%",
    borderWidth: 1,
    borderColor: "#ccc",
    borderRadius: 8,
    paddingHorizontal: 12,
    paddingVertical: 10,
    marginBottom: 16,
  },
  message: {
    fontSize: 18,
  },
});
```

## Vantagens do padrão com hook personalizado

Criar hooks como `useTheme()` e `useAuth()` deixa o consumo do contexto mais limpo e evita importações repetitivas do objeto bruto do contexto.

## Limites da Context API

Ela é ótima para estados globais simples ou médios. Porém, conforme a complexidade cresce, você pode precisar de mais organização, persistência ou otimização.

Por isso, o mais importante aqui é aprender o conceito:

* um provider envolve a árvore;
* o valor é compartilhado;
* os componentes consomem esse valor sem prop drilling.

## Conclusão

Context API é uma solução excelente para compartilhar dados importantes em um app React Native. Quando usada com clareza, ela melhora bastante a organização da aplicação e reduz o excesso de props atravessando componentes.
