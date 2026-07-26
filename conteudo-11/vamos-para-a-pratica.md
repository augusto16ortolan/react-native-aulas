# Vamos para a prática?

<figure><img src="../.gitbook/assets/165238eb-4601-4aae-b8ad-6dc322811aca_text.gif" alt=""><figcaption></figcaption></figure>

Vamos montar um exemplo de CRUD usando React Native com Expo e uma API HTTP.

O objetivo aqui é mostrar o fluxo completo:

* listar tarefas;
* criar tarefas;
* atualizar o status;
* excluir tarefas.

## Estrutura sugerida

```text
src/
  services/
    api.js
  screens/
    TasksScreen.js
```

## Configuração inicial

Se você ainda não tiver um projeto:

```bash
npx create-expo-app@latest tarefas-app
cd tarefas-app
npm install axios
```

## Criando o serviço de API

### `src/services/api.js`

```javascript
import axios from "axios";

export const api = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com",
  headers: {
    "Content-Type": "application/json",
  },
});
```

## Tela de tarefas

### `src/screens/TasksScreen.js`

```jsx
import { useEffect, useState } from "react";
import {
  View,
  Text,
  FlatList,
  TextInput,
  Button,
  Pressable,
  StyleSheet,
  Alert,
} from "react-native";
import { api } from "../services/api";

export default function TasksScreen() {
  const [tasks, setTasks] = useState([]);
  const [newTask, setNewTask] = useState("");
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    loadTasks();
  }, []);

  async function loadTasks() {
    try {
      const response = await api.get("/todos?_limit=8");
      setTasks(response.data);
    } catch (error) {
      console.error(error);
      Alert.alert("Erro", "Não foi possível carregar as tarefas.");
    } finally {
      setLoading(false);
    }
  }

  async function addTask() {
    if (!newTask.trim()) {
      Alert.alert("Atenção", "Digite uma tarefa.");
      return;
    }

    try {
      const response = await api.post("/todos", {
        title: newTask,
        completed: false,
        userId: 1,
      });

      setTasks((currentTasks) => [
        { ...response.data, id: Date.now() },
        ...currentTasks,
      ]);
      setNewTask("");
    } catch (error) {
      console.error(error);
      Alert.alert("Erro", "Não foi possível criar a tarefa.");
    }
  }

  async function toggleTask(task) {
    try {
      await api.patch(`/todos/${task.id}`, {
        completed: !task.completed,
      });

      setTasks((currentTasks) =>
        currentTasks.map((item) =>
          item.id === task.id
            ? { ...item, completed: !item.completed }
            : item
        )
      );
    } catch (error) {
      console.error(error);
      Alert.alert("Erro", "Não foi possível atualizar a tarefa.");
    }
  }

  async function deleteTask(id) {
    try {
      await api.delete(`/todos/${id}`);
      setTasks((currentTasks) => currentTasks.filter((item) => item.id !== id));
    } catch (error) {
      console.error(error);
      Alert.alert("Erro", "Não foi possível remover a tarefa.");
    }
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Lista de Tarefas</Text>

      <TextInput
        style={styles.input}
        placeholder="Nova tarefa"
        value={newTask}
        onChangeText={setNewTask}
      />
      <Button title="Adicionar Tarefa" onPress={addTask} />

      {loading ? (
        <Text style={styles.feedback}>Carregando tarefas...</Text>
      ) : (
        <FlatList
          data={tasks}
          keyExtractor={(item) => item.id.toString()}
          contentContainerStyle={styles.list}
          renderItem={({ item }) => (
            <View style={styles.taskCard}>
              <Pressable onPress={() => toggleTask(item)} style={styles.taskInfo}>
                <Text
                  style={[
                    styles.taskText,
                    item.completed && styles.completedTask,
                  ]}
                >
                  {item.title}
                </Text>
                <Text style={styles.taskStatus}>
                  {item.completed ? "Concluída" : "Pendente"}
                </Text>
              </Pressable>

              <Pressable onPress={() => deleteTask(item.id)}>
                <Text style={styles.deleteButton}>Excluir</Text>
              </Pressable>
            </View>
          )}
        />
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: "#fff",
  },
  title: {
    fontSize: 24,
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
  feedback: {
    marginTop: 20,
  },
  list: {
    paddingTop: 16,
    gap: 12,
  },
  taskCard: {
    borderWidth: 1,
    borderColor: "#ddd",
    borderRadius: 10,
    padding: 14,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
  },
  taskInfo: {
    flex: 1,
    marginRight: 12,
  },
  taskText: {
    fontSize: 16,
    fontWeight: "600",
  },
  completedTask: {
    textDecorationLine: "line-through",
    color: "#6b7280",
  },
  taskStatus: {
    marginTop: 4,
    fontSize: 12,
    color: "#6b7280",
  },
  deleteButton: {
    color: "#b91c1c",
    fontWeight: "700",
  },
});
```

## O que esse exemplo ensina

* **Read**: `loadTasks()` usa `GET`
* **Create**: `addTask()` usa `POST`
* **Update**: `toggleTask()` usa `PATCH`
* **Delete**: `deleteTask()` usa `DELETE`

## Observação importante

O endpoint `jsonplaceholder.typicode.com` é ótimo para estudo, mas ele não salva dados de forma permanente como um backend real. Ele serve para praticar o fluxo de integração sem precisar montar servidor logo no início.

## Conclusão

Esse exemplo já aproxima bastante o aluno de um app real: tela, formulário, lista, atualização de estado local e comunicação com API. É um excelente ponto de transição para integrar o mesmo fluxo com Supabase depois.
