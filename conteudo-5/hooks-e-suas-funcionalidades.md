---
description: >-
  Explore os Hooks do React Native e como eles permitem gerenciar estado e
  efeitos colaterais de forma mais eficiente.
---

# Hooks e suas funcionalidades

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Os hooks foram introduzidos no React para permitir que os desenvolvedores utilizem o estado e outras funcionalidades do React sem a necessidade de escrever classes. Eles são funções especiais que permitem "conectar" as funcionalidades do React ao seu código de forma mais simples e direta. Isso torna o código mais legível e fácil de manter.

Vamos focar em quatro hooks fundamentais: `useState`, `useEffect`, `useLayoutEffect` e `useContext`. Vamos explicar para que cada um serve e fornecer exemplos práticos em React Native para que você possa entender como usá-los em suas aplicações.

### useState

O `useState` é um hook que permite adicionar estado aos componentes funcionais. Ele retorna um par de valores: o estado atual e uma função para atualizá-lo.

Vamos criar um contador simples que incrementa um valor cada vez que um botão é pressionado.

```jsx
import React, { useState } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

export default function App() {
  // Declara uma nova variável de estado, "count", com valor inicial 0
  const [count, setCount] = useState(0);

  return (
    <View style={styles.container}>
      <Text>Você clicou {count} vezes</Text>
      <Button
        title="Clique aqui"
        onPress={() => setCount(count + 1)} // Atualiza o estado "count" incrementando seu valor
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

**Passo a passo**:

1. Importamos o `useState` do React.
2. Utilizamos o `useState` para declarar uma variável de estado chamada `count` e uma função para atualizá-la, `setCount`.
3. O estado inicial de `count` é 0.
4. No evento `onPress` do botão, chamamos `setCount` para incrementar o valor de `count`.

### useEffect

O `useEffect` é um hook que permite executar efeitos colaterais em componentes funcionais. Alguns exemplos de efeitos colaterais são: buscar dados, configurar uma assinatura ou atualizar o DOM. Ele é executado após a renderização do componente.

Vamos buscar dados de uma API e exibi-los na tela.

```jsx
import React, { useState, useEffect } from 'react';
import { View, Text, ActivityIndicator, StyleSheet } from 'react-native';

export default function App() {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch('https://jsonplaceholder.typicode.com/posts/1')
      .then((response) => response.json())
      .then((json) => {
        setData(json);
        setLoading(false);
      });
  }, []); // O array vazio [] significa que este efeito roda apenas uma vez após a primeira renderização

  if (loading) {
    return <ActivityIndicator size="large" color="#0000ff" />;
  }

  return (
    <View style={styles.container}>
      <Text>{data.title}</Text>
      <Text>{data.body}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
  },
});
```

**Passo a passo**:

1. Importamos o `useState` e `useEffect` do React.
2. Utilizamos `useState` para declarar as variáveis de estado `data` (dados da API) e `loading` (indicador de carregamento).
3. Utilizamos `useEffect` para buscar dados da API quando o componente é montado.
4. Quando os dados são recebidos, atualizamos o estado `data` e `loading`.
5. Se ainda estivermos carregando, mostramos um indicador de carregamento (`ActivityIndicator`).
6. Caso contrário, exibimos os dados da API.

### useLayoutEffect

O `useLayoutEffect` é semelhante ao `useEffect`, mas ele é executado de forma síncrona após todas as mutações do DOM. Isso é útil quando você precisa realizar medições de layout ou atualizações do DOM antes da pintura.

Vamos ajustar um layout com base na largura de um componente.

```jsx
import React, { useState, useLayoutEffect, useRef } from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function App() {
  const [width, setWidth] = useState(0);
  const viewRef = useRef(null);

  useLayoutEffect(() => {
    viewRef.current.measure((x, y, w, h) => {
      setWidth(w);
    });
  }, []);

  return (
    <View style={styles.container}>
      <View ref={viewRef} style={styles.box}>
        <Text>A largura da caixa é: {width}</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  box: {
    width: 200,
    height: 100,
    backgroundColor: 'lightblue',
    justifyContent: 'center',
    alignItems: 'center',
  },
});
```

**Passo a passo**:

1. Importamos o `useState`, `useLayoutEffect` e `useRef` do React.
2. Utilizamos `useState` para declarar a variável de estado `width`.
3. Utilizamos `useRef` para criar uma referência para a `View`.
4. Utilizamos `useLayoutEffect` para medir a largura da `View` após a renderização e atualizar o estado `width`.

### useContext

O `useContext` é um hook que permite acessar o contexto do React. O contexto é uma forma de passar dados através da árvore de componentes sem precisar passar explicitamente as props em cada nível.

Vamos criar um contexto de tema e usá-lo em componentes.

```jsx
import React, { useState, useContext, createContext } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';

// Cria um contexto de tema
const ThemeContext = createContext();

export default function App() {
  const [theme, setTheme] = useState('light');

  return (
    <ThemeContext.Provider value={theme}>
      <View style={styles.container}>
        <ThemeToggle />
        <Button title="Trocar Tema" onPress={() => setTheme(theme === 'light' ? 'dark' : 'light')} />
      </View>
    </ThemeContext.Provider>
  );
}

function ThemeToggle() {
  const theme = useContext(ThemeContext);
  return (
    <View style={theme === 'light' ? styles.light : styles.dark}>
      <Text>O tema atual é {theme}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  light: {
    padding: 20,
    backgroundColor: '#fff',
  },
  dark: {
    padding: 20,
    backgroundColor: '#333',
    color: '#fff',
  },
});
```

**Passo a passo**:

1. Importamos o `useState`, `useContext` e `createContext` do React.
2. Criamos um contexto de tema com `createContext`.
3. Utilizamos `useState` para declarar a variável de estado `theme`.
4. Usamos `ThemeContext.Provider` para fornecer o valor do tema aos componentes filhos.
5. Criamos um componente `ThemeToggle` que usa `useContext` para acessar o valor do tema e exibir o tema atual.

### Conclusão

Os hooks são uma poderosa adição ao React, permitindo que os desenvolvedores gerenciem estado e outros recursos de forma mais eficiente e direta. Com `useState`, você pode adicionar e gerenciar estado local em componentes funcionais. Com `useEffect` e `useLayoutEffect`, você pode lidar com efeitos colaterais e atualizações de layout. E com `useContext`, você pode acessar dados de contexto sem precisar passar props manualmente por cada nível da árvore de componentes. Dominar esses hooks é fundamental para criar aplicativos React Native robustos e eficientes.
