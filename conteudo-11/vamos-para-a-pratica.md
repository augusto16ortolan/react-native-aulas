# Vamos para a prática?

<figure><img src="../.gitbook/assets/165238eb-4601-4aae-b8ad-6dc322811aca_text.gif" alt=""><figcaption></figcaption></figure>

Vamos seguir com uma abordagem prática para demonstrar a integração de um aplicativo React Native com um backend usando uma lista de tarefas como exemplo. Vou usar a biblioteca **axios** para simplificar as requisições HTTP e mostrar como criar operações CRUD completas (Create, Read, Update, Delete).

## Exemplo prático: lista de tarefas

### Configuração incial

Primeiro, certifique-se de ter um projeto Expo configurado. Se ainda não tiver, você pode criar um usando o seguinte comando:

```bash
npx expo init TarefasApp
cd TarefasApp
npm install axios
```

### Estrutura do backend (endpoints/rotas)

Para fins de demonstração, vamos supor que o backend esteja disponível no endpoint `https://meuservidor.com/api/tarefas`. Aqui estão os endpoints que serão usados:

* **GET** `/api/tarefas` - Retorna uma lista de todas as tarefas.
* **POST** `/api/tarefas` - Cria uma nova tarefa.
* **PUT** `/api/tarefas/:id` - Atualiza uma tarefa existente.
* **DELETE** `/api/tarefas/:id` - Remove uma tarefa.

### Configurando o frontend com React Native

#### Criando components e configurando o Axios

Vamos criar uma pasta chamada `src` e dentro dela, adicionar um arquivo para configurar o Axios:

src/api.js

```javascript
import axios from 'axios';

const api = axios.create({
  baseURL: 'https://meuservidor.com/api'
});

export default api;
```

#### Criando tela de lista de tarefas

src/screens/TarefasScreen.js

```jsx
import React, { useState, useEffect } from 'react';
import { View, Text, FlatList, Button, TextInput, TouchableOpacity, StyleSheet } from 'react-native';
import api from '../api';

const TarefasScreen = () => {
  const [tarefas, setTarefas] = useState([]);
  const [novaTarefa, setNovaTarefa] = useState('');

  useEffect(() => {
    fetchTarefas();
  }, []);

  const fetchTarefas = async () => {
    try {
      const response = await api.get('/tarefas');
      setTarefas(response.data);
    } catch (error) {
      console.error("Erro ao buscar tarefas:", error);
    }
  };

  const adicionarTarefa = async () => {
    if (!novaTarefa) return;

    try {
      const response = await api.post('/tarefas', { titulo: novaTarefa });
      setTarefas([...tarefas, response.data]);
      setNovaTarefa('');
    } catch (error) {
      console.error("Erro ao adicionar tarefa:", error);
    }
  };

  const removerTarefa = async (id) => {
    try {
      await api.delete(`/tarefas/${id}`);
      setTarefas(tarefas.filter(tarefa => tarefa.id !== id));
    } catch (error) {
      console.error("Erro ao remover tarefa:", error);
    }
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Lista de Tarefas</Text>
      
      <TextInput
        style={styles.input}
        placeholder="Nova tarefa"
        value={novaTarefa}
        onChangeText={setNovaTarefa}
      />
      <Button title="Adicionar Tarefa" onPress={adicionarTarefa} />
      
      <FlatList
        data={tarefas}
        keyExtractor={(item) => item.id.toString()}
        renderItem={({ item }) => (
          <View style={styles.taskContainer}>
            <Text style={styles.taskText}>{item.titulo}</Text>
            <TouchableOpacity onPress={() => removerTarefa(item.id)}>
              <Text style={styles.deleteButton}>Excluir</Text>
            </TouchableOpacity>
          </View>
        )}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#fff'
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    marginBottom: 10
  },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    padding: 10,
    marginBottom: 10
  },
  taskContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    padding: 10,
    borderBottomWidth: 1,
    borderColor: '#ccc'
  },
  taskText: {
    fontSize: 18
  },
  deleteButton: {
    color: 'red'
  }
});

export default TarefasScreen;

```

### Explicação do código

* **Configuração do Axios**: A função `api` é configurada com uma `baseURL`, que será usada para fazer todas as requisições HTTP. Isso facilita na hora de adicionar endpoints.
* **Buscar Tarefas (`GET`)**: Quando o componente é carregado, ele usa `fetchTarefas` para buscar a lista de tarefas do servidor. Isso é feito usando a função `api.get()`.
* **Adicionar Nova Tarefa (`POST`)**: A função `adicionarTarefa` envia uma requisição `POST` para criar uma nova tarefa. Se a requisição for bem-sucedida, a nova tarefa é adicionada ao estado `tarefas`.
* **Remover Tarefa (`DELETE`)**: A função `removerTarefa` usa `api.delete()` para excluir uma tarefa no servidor. O ID da tarefa é passado na URL.
* **Componentes de Interface**: Usamos `FlatList` para renderizar a lista de tarefas e um `TextInput` para adicionar novas tarefas. Botões de ação (`Button`, `TouchableOpacity`) permitem adicionar e excluir tarefas.
