---
description: >-
  Explore os hooks mais importantes do React para gerenciar estado, efeitos e
  compartilhamento de dados em aplicativos React Native.
---

# Hooks e suas funcionalidades

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Hooks são funções especiais do React que permitem usar recursos como estado, efeitos e contexto em componentes funcionais.

No React Native moderno, eles são parte do fluxo normal de desenvolvimento. Saber usar hooks bem é essencial para construir telas que:

* respondem à interação do usuário;
* carregam dados;
* atualizam a interface;
* compartilham informações entre componentes.

## `useState`

`useState` cria estado local dentro de um componente.

```jsx
import { useState } from "react";
import { View, Text, Button, StyleSheet } from "react-native";

export default function App() {
  const [count, setCount] = useState(0);

  return (
    <View style={styles.container}>
      <Text>Você clicou {count} vezes</Text>
      <Button title="Clique aqui" onPress={() => setCount(count + 1)} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    gap: 12,
  },
});
```

Use `useState` para valores que mudam ao longo da vida da tela, como:

* texto digitado;
* loading;
* lista carregada da API;
* item selecionado.

## `useEffect`

`useEffect` executa efeitos colaterais depois da renderização do componente.

Exemplos de efeito colateral:

* buscar dados;
* ouvir eventos;
* iniciar timers;
* sincronizar algo com uma API.

```jsx
import { useEffect, useState } from "react";
import { View, Text, ActivityIndicator, StyleSheet } from "react-native";

export default function App() {
  const [post, setPost] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    async function fetchPost() {
      try {
        const response = await fetch(
          "https://jsonplaceholder.typicode.com/posts/1"
        );
        const json = await response.json();
        setPost(json);
      } catch (err) {
        setError("Não foi possível carregar os dados.");
      } finally {
        setLoading(false);
      }
    }

    fetchPost();
  }, []);

  if (loading) {
    return <ActivityIndicator style={styles.center} size="large" color="#1f3c88" />;
  }

  if (error) {
    return (
      <View style={styles.center}>
        <Text>{error}</Text>
      </View>
    );
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>{post.title}</Text>
      <Text>{post.body}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  center: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  container: {
    flex: 1,
    justifyContent: "center",
    padding: 20,
  },
  title: {
    fontSize: 20,
    fontWeight: "700",
    marginBottom: 12,
  },
});
```

O array vazio `[]` faz o efeito rodar apenas na montagem inicial da tela.

## `useLayoutEffect`

`useLayoutEffect` é parecido com `useEffect`, mas roda em um momento mais cedo do ciclo de atualização da interface.

Em React Native, ele é muito usado quando queremos configurar a tela assim que ela é exibida, por exemplo em navegação.

```jsx
import { useLayoutEffect } from "react";
import { View, Text } from "react-native";

export default function DetailsScreen({ navigation }) {
  useLayoutEffect(() => {
    navigation.setOptions({
      title: "Detalhes do Produto",
    });
  }, [navigation]);

  return (
    <View>
      <Text>Tela de detalhes</Text>
    </View>
  );
}
```

Para iniciantes, essa costuma ser uma aplicação mais útil e realista do que exemplos de medição manual de layout.

## `useContext`

`useContext` permite acessar valores de um contexto React sem precisar passar props em vários níveis.

```jsx
import { createContext, useContext, useState } from "react";
import { View, Text, Button, StyleSheet } from "react-native";

const ThemeContext = createContext();

function ThemeProvider({ children }) {
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

function ThemeCard() {
  const { theme, toggleTheme } = useContext(ThemeContext);
  const isDark = theme === "dark";

  return (
    <View
      style={[
        styles.card,
        { backgroundColor: isDark ? "#1f2937" : "#f3f4f6" },
      ]}
    >
      <Text style={{ color: isDark ? "#fff" : "#111" }}>
        Tema atual: {theme}
      </Text>
      <Button title="Alternar tema" onPress={toggleTheme} />
    </View>
  );
}

export default function App() {
  return (
    <ThemeProvider>
      <View style={styles.container}>
        <ThemeCard />
      </View>
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
  card: {
    width: "100%",
    padding: 20,
    borderRadius: 12,
    gap: 12,
  },
});
```

## Quando usar cada hook

* **`useState`**: para estado local da tela ou componente.
* **`useEffect`**: para buscar dados, ouvir eventos e sincronizar efeitos.
* **`useLayoutEffect`**: para ajustes que precisam acontecer junto da configuração visual, como cabeçalho de navegação.
* **`useContext`**: para compartilhar valores entre vários componentes.

## Conclusão

Hooks são a espinha dorsal do React moderno. Dominar bem esses quatro já permite construir telas dinâmicas, formular interações, carregar dados externos e organizar estados compartilhados com muito mais clareza.
