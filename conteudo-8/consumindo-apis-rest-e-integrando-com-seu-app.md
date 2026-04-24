---
description: >-
  Conectando seu aplicativo a APIs REST para buscar e enviar dados. Vamos
  explorar técnicas para fazer requisições, manipular respostas e integrar essas
  funcionalidades de forma eficiente em seu app.
---

# Consumindo APIs REST e integrando com seu app

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Se você já está familiarizado com o que é uma API (Interface de Programação de Aplicações), agora vamos explorar como consumir uma API REST em seu aplicativo React Native. Usaremos o **Axios**, uma biblioteca popular para realizar requisições HTTP, que facilita a comunicação com APIs e o tratamento de respostas.

### Configurando o axios

Para começar a usar o Axios em seu projeto, você precisa instalá-lo. No terminal, execute:

```jsx
npm install axios
```

### Realizando requisições com axios

O Axios facilita a realização de requisições HTTP e o tratamento das respostas. Vamos ver alguns exemplos de como usar o Axios para fazer chamadas a uma API REST.

#### Fazendo uma requisição GET

Uma requisição GET é usada para buscar dados de um servidor. Vamos buscar uma lista de usuários fictícios de uma API.

```jsx
import React, { useState, useEffect } from 'react';
import { View, Text, StyleSheet, FlatList, Alert } from 'react-native';
import axios from 'axios';

export default function UserList() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    const fetchUsers = async () => {
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/users');
        setUsers(response.data);
      } catch (error) {
        console.error('Erro ao buscar os dados', error);
        Alert.alert('Erro', 'Não foi possível carregar os dados.');
      }
    };

    fetchUsers();
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.header}>Lista de Usuários</Text>
      <FlatList
        data={users}
        keyExtractor={item => item.id.toString()}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{item.name}</Text>
            <Text>{item.email}</Text>
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
    marginBottom: 10,
  },
  item: {
    padding: 10,
    borderBottomWidth: 1,
    borderBottomColor: '#ccc',
  },
});
```

**O que está acontecendo aqui?**

* **`axios.get()`**: Envia uma requisição GET para a URL especificada.
* **`useEffect()`**: Utilizado para buscar os dados assim que o componente é montado.
* **`setUsers()`**: Atualiza o estado com a lista de usuários recebida.
* **`FlatList`**: Exibe a lista de usuários na tela.

#### Fazendo uma requisição POST

Uma requisição POST é usada para enviar dados ao servidor. Vamos criar um novo usuário fictício.

```jsx
import React, { useState } from 'react';
import { View, Text, TextInput, Button, StyleSheet, Alert } from 'react-native';
import axios from 'axios';

export default function CreateUser() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');

  const handleSubmit = async () => {
    try {
      const response = await axios.post('https://jsonplaceholder.typicode.com/users', {
        name,
        email,
      });
      Alert.alert('Usuário criado com sucesso!', `Nome: ${response.data.name}`);
    } catch (error) {
      console.error('Erro ao criar usuário', error);
      Alert.alert('Erro', 'Não foi possível criar o usuário.');
    }
  };

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
  },
  header: {
    fontSize: 20,
    marginBottom: 10,
  },
  input: {
    height: 40,
    borderColor: '#ccc',
    borderWidth: 1,
    marginBottom: 10,
    paddingHorizontal: 8,
  },
});
```

**O que está acontecendo aqui?**

* **`axios.post()`**: Envia uma requisição POST para a URL especificada com os dados do novo usuário.
* **`handleSubmit()`**: Função que é chamada quando o botão é pressionado.
* **`Alert.alert()`**: Exibe uma mensagem de sucesso.

### Conclusão

Consumir APIs REST é uma habilidade essencial no desenvolvimento de aplicativos móveis. Com o Axios, você pode fazer requisições HTTP para buscar ou enviar dados de forma simples e eficiente. Lembre-se de sempre tratar os erros e garantir uma boa experiência do usuário, mesmo quando as coisas não saem como planejado.
