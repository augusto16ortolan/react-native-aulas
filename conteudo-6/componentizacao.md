---
description: >-
  Descubra como dividir seu aplicativo em componentes reutilizáveis e bem
  organizados no React Native.
---

# Componentização

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

Componentizar significa quebrar a interface em partes menores, reutilizáveis e com responsabilidade clara.

Em vez de criar uma tela gigante com tudo misturado, nós separamos o projeto em peças menores, como:

* botões;
* cards;
* campos de formulário;
* cabeçalhos;
* itens de lista.

## Por que componentizar?

* **Reutilização**: o mesmo componente pode aparecer em várias telas.
* **Organização**: cada parte da interface fica em um lugar previsível.
* **Manutenção**: fica mais fácil corrigir ou melhorar um trecho do app.
* **Leitura**: uma tela grande fica muito mais clara quando delega partes para componentes menores.

## Exemplo: criando um botão reutilizável

Vamos criar um componente chamado `CustomButton.js`.

```jsx
import { Pressable, Text, StyleSheet } from "react-native";

export default function CustomButton({ title, onPress }) {
  return (
    <Pressable style={styles.button} onPress={onPress}>
      <Text style={styles.text}>{title}</Text>
    </Pressable>
  );
}

const styles = StyleSheet.create({
  button: {
    backgroundColor: "#1f3c88",
    paddingVertical: 14,
    paddingHorizontal: 18,
    borderRadius: 8,
    alignItems: "center",
  },
  text: {
    color: "#fff",
    fontSize: 16,
    fontWeight: "600",
  },
});
```

Agora vamos usar esse componente no `App.js`.

```jsx
import { Alert, View, Text, StyleSheet } from "react-native";
import CustomButton from "./CustomButton";

export default function App() {
  function handlePress() {
    Alert.alert("Ação", "Botão pressionado!");
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Bem-vindo ao Meu App!</Text>
      <CustomButton title="Clique aqui" onPress={handlePress} />
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
    marginBottom: 20,
    fontWeight: "700",
  },
});
```

## O que esse exemplo ensina

### Separação de responsabilidade

O botão sabe renderizar o botão.

O `App` sabe quando ele deve ser usado e qual ação dispara.

### Reutilização com props

O componente recebe:

* `title`
* `onPress`

Essas props permitem usar o mesmo botão em vários contextos diferentes sem duplicar a estrutura.

## Estrutura comum em projetos

Conforme o app cresce, uma organização comum é:

```text
src/
  components/
    CustomButton.js
    UserCard.js
  screens/
    HomeScreen.js
    DetailsScreen.js
```

Essa separação ajuda a distinguir:

* componentes reutilizáveis;
* telas completas;
* arquivos de serviço e lógica.

## Quando um trecho merece virar componente?

Pergunte:

* esse bloco será repetido?
* esse trecho já está deixando a tela longa demais?
* essa parte possui um visual ou comportamento próprio?

Se a resposta for “sim” para alguma dessas perguntas, provavelmente vale componentizar.

## Conclusão

Componentização não é só uma técnica de organização. Ela é uma forma de pensar a interface em blocos consistentes, reaproveitáveis e mais fáceis de evoluir. Em React Native, isso é essencial para manter o projeto saudável conforme ele cresce.
