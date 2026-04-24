---
description: >-
  Descubra como dividir seu aplicativo em componentes reutilizáveis e
  independentes no React Native.
---

# Componentização

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Componentização é um conceito fundamental no React Native que ajuda a organizar e estruturar seu código de forma eficiente. Em vez de escrever grandes blocos de código para a interface do usuário, você divide a aplicação em partes menores chamadas **componentes**. Cada componente é responsável por uma parte específica da interface e pode ser reutilizado em diferentes partes do aplicativo.

A seguir, vamos explorar o que é componentização, como ela funciona e como você pode usá-la para tornar seu código mais organizado e fácil de manter.

No React Native, um **componente** é uma função ou classe que retorna uma parte da interface do usuário. Cada componente pode ter seu próprio estilo e lógica, e pode ser reutilizado em diferentes lugares do seu aplicativo.

### Por que componentizar?

* **Reutilização**: Você pode usar o mesmo componente em várias partes da aplicação, evitando a duplicação de código.
* **Manutenção**: Código dividido em componentes menores é mais fácil de entender e manter.
* **Organização**: Ajuda a manter o código organizado e modular, facilitando o trabalho em equipe.

### Passo a passo para criar componentes

Vamos criar um botão reutilizável que pode ser usado em diferentes partes da nossa aplicação.

Primeiro, devemos criar o arquivo do componente. Vamos chamá-lo de `CustomButton.js`.

```jsx
// CustomButton.js
import React from 'react';
import { TouchableOpacity, Text, StyleSheet } from 'react-native';

// Componente CustomButton
const CustomButton = ({ title, onPress }) => {
  return (
    <TouchableOpacity style={styles.button} onPress={onPress}>
      <Text style={styles.text}>{title}</Text>
    </TouchableOpacity>
  );
};

// Estilos para o componente CustomButton
const styles = StyleSheet.create({
  button: {
    backgroundColor: '#007BFF',
    padding: 10,
    borderRadius: 5,
    alignItems: 'center',
  },
  text: {
    color: '#FFFFFF',
    fontSize: 16,
  },
});

// Exporta o componente para que possa ser usado em outros arquivos
export default CustomButton;

```

Agora, vamos usar o `CustomButton` em nosso componente principal, que será o `App.js`.

```jsx
// App.js
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';
import CustomButton from './CustomButton'; // Importa o componente CustomButton

export default function App() {
  // Função chamada quando o botão é pressionado
  const handlePress = () => {
    alert('Botão pressionado!');
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Bem-vindo ao Meu App!</Text>
      <CustomButton title="Clique Aqui" onPress={handlePress} />
    </View>
  );
}

// Estilos para o componente App
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
});
```

#### Explicação do Exemplo

1. **Criação do Componente**:
   * **`CustomButton.js`**: Criamos um componente funcional que retorna um botão estilizado. Este componente recebe duas propriedades (`title` e `onPress`). O botão é estilizado com `StyleSheet`, e o texto é exibido dentro do botão.
2. **Importação e Uso**:
   * **`App.js`**: Importamos o `CustomButton` e o utilizamos dentro do componente `App`. Passamos as propriedades `title` e `onPress` para personalizar o botão.

#### Benefícios da Componentização

* **Facilidade de Manutenção**: Alterações no `CustomButton` serão refletidas em todos os lugares onde ele é usado, facilitando a manutenção e atualização.
* **Organização do Código**: Mantém seu código limpo e organizado, dividindo-o em partes menores e mais gerenciáveis.
* **Reutilização**: Permite criar componentes reutilizáveis que economizam tempo e reduzem a duplicação de código.

### Conclusão

A componentização é uma prática essencial no desenvolvimento com React Native. Ao dividir a interface em componentes menores e reutilizáveis, você melhora a organização, facilita a manutenção e torna o código mais legível. Experimente criar seus próprios componentes e veja como eles podem simplificar o desenvolvimento de aplicativos complexos.
