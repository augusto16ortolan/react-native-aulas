---
description: >-
  Como consumir dados com Axios, paralelizar requisições com Promise.all e
  organizar melhor a carga de dados em tela.
---

# APIs no React Native com Axios e Promise.all

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Quando uma tela depende de mais de uma requisição, uma boa estratégia é rodá-las em paralelo.

## Por que usar Axios?

Axios ajuda bastante em:

* clareza de leitura;
* configuração de `baseURL`;
* envio de `params`;
* tratamento de resposta.

## O papel do `Promise.all`

`Promise.all` permite:

* iniciar várias requisições ao mesmo tempo;
* esperar todas terminarem;
* seguir o fluxo só quando tudo estiver pronto.

Se uma das promises falhar, o `catch` é acionado.

## Exemplo

```jsx
import { useEffect, useState } from "react";
import { View, Text, StyleSheet, FlatList, Alert, Image } from "react-native";
import axios from "axios";

export default function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    async function fetchUsers() {
      try {
        const [brRes, usRes] = await Promise.all([
          axios.get("https://randomuser.me/api/", {
            params: { results: 5, nat: "br" },
          }),
          axios.get("https://randomuser.me/api/", {
            params: { results: 5, nat: "us" },
          }),
        ]);

        const merged = [...brRes.data.results, ...usRes.data.results];
        setUsers(merged);
      } catch (error) {
        console.error(error);
        Alert.alert("Erro", "Não foi possível carregar os usuários.");
      }
    }

    fetchUsers();
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Lista de Usuários</Text>
      <FlatList
        data={users}
        keyExtractor={(item) => item.login.uuid}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Image source={{ uri: item.picture.thumbnail }} style={styles.avatar} />
            <View>
              <Text style={styles.name}>
                {item.name.first} {item.name.last}
              </Text>
              <Text>{item.email}</Text>
            </View>
          </View>
        )}
      />
    </View>
  );
}

const styles = StyleSheet.create({
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
    flexDirection: "row",
    alignItems: "center",
    gap: 10,
    paddingVertical: 10,
    borderBottomWidth: 1,
    borderBottomColor: "#ddd",
  },
  avatar: {
    width: 40,
    height: 40,
    borderRadius: 20,
  },
  name: {
    fontWeight: "600",
  },
});
```

## Quando usar com cuidado

`Promise.all` é ótimo quando todas as respostas são obrigatórias. Se você quiser tolerar falhas parciais, pode estudar `Promise.allSettled`.

## Conclusão

Esse padrão ajuda muito na construção de telas que dependem de múltiplas fontes de dados e melhora a organização do fluxo assíncrono.
