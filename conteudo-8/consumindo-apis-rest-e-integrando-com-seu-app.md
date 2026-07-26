---
description: >-
  Conectando seu aplicativo a APIs REST para buscar e enviar dados com boas
  práticas de loading, erro e organização.
---

# Consumindo APIs REST e integrando com seu app

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Consumir APIs é uma parte central de muitos aplicativos. É assim que o app:

* busca usuários;
* lista produtos;
* envia formulários;
* salva tarefas;
* sincroniza informações com o servidor.

Neste capítulo, vamos usar **Axios**, porque ele deixa o código claro e muito usado no mercado.

## Instalando o Axios

```bash
npm install axios
```

## Exemplo prático: listando usuários

```jsx
import { useEffect, useState } from "react";
import {
  View,
  Text,
  StyleSheet,
  FlatList,
  Alert,
  ActivityIndicator,
} from "react-native";
import axios from "axios";

export default function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    async function fetchUsers() {
      try {
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/users"
        );
        setUsers(response.data);
      } catch (error) {
        console.error("Erro ao buscar usuários:", error);
        Alert.alert("Erro", "Não foi possível carregar os dados.");
      } finally {
        setLoading(false);
      }
    }

    fetchUsers();
  }, []);

  if (loading) {
    return (
      <View style={styles.center}>
        <ActivityIndicator size="large" color="#1f3c88" />
      </View>
    );
  }

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Lista de Usuários</Text>
      <FlatList
        data={users}
        keyExtractor={(item) => item.id.toString()}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text style={styles.name}>{item.name}</Text>
            <Text>{item.email}</Text>
          </View>
        )}
      />
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
    padding: 20,
  },
  header: {
    fontSize: 20,
    fontWeight: "700",
    marginBottom: 12,
  },
  item: {
    paddingVertical: 12,
    borderBottomWidth: 1,
    borderBottomColor: "#ddd",
  },
  name: {
    fontWeight: "600",
  },
});
```

## O que esse exemplo mostra

* `axios.get()` faz a requisição;
* `useEffect()` dispara a busca quando a tela abre;
* `loading` controla o estado de carregamento;
* `try/catch` trata falhas;
* `FlatList` renderiza os dados.

## Exemplo prático: enviando dados com `POST`

```jsx
import { useState } from "react";
import {
  View,
  Text,
  TextInput,
  Button,
  StyleSheet,
  Alert,
} from "react-native";
import axios from "axios";

export default function CreateUser() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");

  async function handleSubmit() {
    if (!name || !email) {
      Alert.alert("Atenção", "Preencha nome e email.");
      return;
    }

    try {
      const response = await axios.post(
        "https://jsonplaceholder.typicode.com/users",
        {
          name,
          email,
        }
      );

      Alert.alert(
        "Usuário criado",
        `Nome retornado pela API: ${response.data.name}`
      );
      setName("");
      setEmail("");
    } catch (error) {
      console.error("Erro ao criar usuário:", error);
      Alert.alert("Erro", "Não foi possível criar o usuário.");
    }
  }

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Criar Novo Usuário</Text>
      <TextInput
        style={styles.input}
        placeholder="Nome"
        value={name}
        onChangeText={setName}
      />
      <TextInput
        style={styles.input}
        placeholder="Email"
        keyboardType="email-address"
        autoCapitalize="none"
        value={email}
        onChangeText={setEmail}
      />
      <Button title="Criar Usuário" onPress={handleSubmit} />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    justifyContent: "center",
  },
  header: {
    fontSize: 20,
    fontWeight: "700",
    marginBottom: 12,
  },
  input: {
    borderWidth: 1,
    borderColor: "#ccc",
    borderRadius: 8,
    paddingHorizontal: 12,
    paddingVertical: 10,
    marginBottom: 12,
  },
});
```

## Próximo nível de organização

Quando o projeto cresce, o ideal é não deixar a URL da API espalhada em vários arquivos. Um padrão comum é criar um arquivo de serviço:

```javascript
import axios from "axios";

export const api = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com",
});
```

Depois:

```javascript
const response = await api.get("/users");
```

## Conclusão

Consumir APIs com Axios em React Native não é só “fazer uma requisição”. O fluxo completo envolve carregar, tratar erro, atualizar interface e organizar o código para crescer sem virar bagunça.
