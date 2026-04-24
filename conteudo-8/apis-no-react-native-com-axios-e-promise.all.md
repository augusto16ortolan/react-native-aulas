---
description: >-
  Como consumir dados com Axios, organizar chamadas assíncronas (incluindo
  Promise.all) e lidar com erros de forma simples.
---

# APIs no React Native com Axios e Promise.all

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

#### Por que usar Axios?

O **Axios** facilita requisições HTTP e deixa o código mais limpo, principalmente para:

* passar `params` (query string) de forma simples
* tratar erros com `try/catch`

#### O que o `Promise.all` resolve?

Quando você precisa de **mais de uma requisição** para montar a tela, o `Promise.all`:

* executa as requisições **ao mesmo tempo**
* só continua quando **todas** terminarem
* se **uma falhar**, cai no `catch`

No exemplo abaixo, buscamos usuários de **duas nacionalidades** (BR e US) em paralelo e juntamos tudo numa lista.

### Praticando...

> Instale: `npm i axios`

```jsx
import React, { useState, useEffect } from "react";
import { View, Text, StyleSheet, FlatList, Alert, Image } from "react-native";
import axios from "axios";

export default function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    const fetchUsers = async () => {
      try {
        // Promise.all: duas requisições em paralelo
        const [brRes, usRes] = await Promise.all([
          axios.get("https://randomuser.me/api/", {
            params: { results: 5, nat: "br" },
          }),
          axios.get("https://randomuser.me/api/", {
            params: { results: 5, nat: "us" },
          }),
        ]);

        // Junta as duas listas em uma só
        const merged = [...brRes.data.results, ...usRes.data.results];
        setUsers(merged);
      } catch (error) {
        console.error("Erro ao buscar os dados", error);
        Alert.alert("Erro", "Não foi possível carregar os dados.");
      }
    };

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
            <Image
              source={{ uri: item.picture.thumbnail }}
              style={styles.avatar}
            />

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
  container: { flex: 1, padding: 20 },
  header: { fontSize: 20, marginBottom: 10, fontWeight: "600" },
  item: {
    paddingVertical: 10,
    borderBottomWidth: 1,
    borderBottomColor: "#ccc",
    flexDirection: "row",
    alignItems: "center",
    gap: 10,
  },
  avatar: { width: 40, height: 40, borderRadius: 20 },
  name: { fontWeight: "600" },
});
```

### Conclusão

Com esse padrão simples, você já cobre o essencial da integração com API no React Native: **buscar dados com Axios**, **tratar erros**, **renderizar em lista** e usar `Promise.all` para **paralelizar requisições** e deixar a tela mais rápida e organizada.
