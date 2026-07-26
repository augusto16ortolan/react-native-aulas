---
description: >-
  Explore bibliotecas de componentes prontos para acelerar o desenvolvimento e
  manter consistência visual no aplicativo.
---

# Bibliotecas de componentes

<figure><img src="../.gitbook/assets/React Native (8).png" alt=""><figcaption></figcaption></figure>

Bibliotecas de componentes ajudam a acelerar a construção da interface. Em vez de criar tudo do zero, você reaproveita componentes já prontos, como:

* botões;
* inputs;
* cards;
* diálogos;
* barras de navegação;
* menus.

Isso pode economizar muito tempo, principalmente em projetos com prazo curto ou com várias telas parecidas.

## Por que usar uma biblioteca?

* **Velocidade**: vários componentes já vêm prontos para uso.
* **Consistência**: o app mantém um padrão visual mais uniforme.
* **Acessibilidade**: muitas bibliotecas já tratam comportamento básico de interação.
* **Produtividade**: sobra mais tempo para focar na lógica do aplicativo.

## Cuidados antes de adotar

Nem sempre a melhor decisão é instalar uma biblioteca só porque ela existe.

Antes de usar, avalie:

* a biblioteca está ativa e bem documentada?
* funciona bem com Expo e com a versão atual do projeto?
* os componentes se encaixam no estilo visual do app?
* vale mais a pena usar a biblioteca inteira ou criar 2 ou 3 componentes próprios?

## Bibliotecas populares

### React Native Paper

O **React Native Paper** é uma das opções mais conhecidas para quem quer trabalhar com componentes inspirados em Material Design.

Exemplo:

```jsx
import { View, StyleSheet } from "react-native";
import { Button, TextInput, Appbar } from "react-native-paper";

export default function App() {
  return (
    <View style={styles.container}>
      <Appbar.Header>
        <Appbar.Content title="Meu App" />
      </Appbar.Header>
      <View style={styles.content}>
        <TextInput label="Digite seu nome" mode="outlined" />
        <Button mode="contained" onPress={() => {}}>
          Enviar
        </Button>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  content: {
    padding: 20,
    gap: 16,
  },
});
```

### RNEUI (evolução do React Native Elements)

O projeto que muita gente conheceu como **React Native Elements** evoluiu para o ecossistema **RNEUI**.

Exemplo:

```jsx
import { View, StyleSheet } from "react-native";
import { Button, Input } from "@rneui/themed";

export default function App() {
  return (
    <View style={styles.container}>
      <Input placeholder="Digite seu nome" />
      <Button title="Enviar" />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    padding: 20,
  },
});
```

## Como instalar

O processo depende da biblioteca escolhida. Por isso, sempre consulte a documentação oficial.

Exemplo com React Native Paper:

```bash
npm install react-native-paper
```

Exemplo com RNEUI:

```bash
npm install @rneui/themed @rneui/base
```

Em projetos Expo, também pode ser necessário instalar dependências compatíveis usando `npx expo install`, dependendo do que a biblioteca pedir.

## Quando criar componentes próprios é melhor

Mesmo com bibliotecas, ainda faz sentido criar componentes próprios quando:

* o visual do projeto é muito específico;
* você só precisa de poucos componentes;
* quer manter o app mais leve;
* deseja entender melhor a construção da interface antes de abstrair demais.

## Estratégia recomendada para a turma

Para aprendizado, uma boa estratégia é:

1. primeiro entender os componentes nativos do React Native;
2. depois criar alguns componentes próprios;
3. só então introduzir uma biblioteca para comparar produtividade e padrão visual.

Assim, a biblioteca vira uma escolha consciente, e não uma muleta.

## Conclusão

Bibliotecas de componentes podem acelerar bastante o desenvolvimento, mas devem ser usadas com critério. Em um bom projeto, elas entram para resolver um problema real: ganhar velocidade, manter consistência e reduzir retrabalho sem esconder o entendimento da base do React Native.
