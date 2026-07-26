# Conhecendo o Supabase

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

O **Supabase** é uma plataforma de backend que combina várias peças muito úteis para aplicativos:

* autenticação;
* banco de dados PostgreSQL;
* APIs geradas a partir do banco;
* armazenamento de arquivos;
* recursos em tempo real.

Para projetos mobile com React Native, ele é especialmente interessante porque reduz bastante a quantidade de infraestrutura que precisaríamos montar manualmente.

## O que o Supabase entrega

### Authentication

Com Supabase Auth, podemos implementar:

* cadastro com email e senha;
* login e logout;
* recuperação de senha;
* persistência de sessão;
* autenticação com provedores externos.

Em aplicativos, isso significa controlar quem pode entrar, quais dados cada pessoa pode acessar e como manter a sessão ativa.

### Database

O banco de dados do Supabase é baseado em **PostgreSQL**.

Isso permite:

* tabelas relacionais;
* filtros;
* ordenação;
* consultas poderosas;
* políticas de segurança com **RLS** (Row Level Security).

Um ponto importante: em Supabase, segurança de dados não depende só do código do app. Ela também depende da configuração correta no banco.

### Storage

O Storage serve para guardar arquivos, como:

* fotos de perfil;
* imagens de produtos;
* documentos;
* anexos.

Ele funciona com buckets e pode ser configurado com acesso público ou privado.

## Instalando no projeto React Native com Expo

Em projetos atuais com Expo, um fluxo comum é:

```bash
npx expo install @supabase/supabase-js @react-native-async-storage/async-storage react-native-url-polyfill
```

## Variáveis de ambiente

No Expo, variáveis usadas no código do app devem começar com `EXPO_PUBLIC_`.

Exemplo de `.env`:

```env
EXPO_PUBLIC_SUPABASE_URL=https://seu-projeto.supabase.co
EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY=sua_chave_publica_aqui
```

## Criando o cliente

Um arquivo comum para iniciar o Supabase seria `lib/supabase.js`:

```jsx
import "react-native-url-polyfill/auto";
import AsyncStorage from "@react-native-async-storage/async-storage";
import { createClient } from "@supabase/supabase-js";

const supabaseUrl = process.env.EXPO_PUBLIC_SUPABASE_URL;
const supabaseKey = process.env.EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY;

export const supabase = createClient(supabaseUrl, supabaseKey, {
  auth: {
    storage: AsyncStorage,
    autoRefreshToken: true,
    persistSession: true,
    detectSessionInUrl: false,
  },
});
```

## Exemplo simples de leitura de dados

```jsx
import { useEffect, useState } from "react";
import { View, Text } from "react-native";
import { supabase } from "./lib/supabase";

export default function App() {
  const [tarefas, setTarefas] = useState([]);

  useEffect(() => {
    async function loadTasks() {
      const { data, error } = await supabase.from("tasks").select("*");

      if (error) {
        console.error(error);
        return;
      }

      setTarefas(data);
    }

    loadTasks();
  }, []);

  return (
    <View>
      {tarefas.map((task) => (
        <Text key={task.id}>{task.title}</Text>
      ))}
    </View>
  );
}
```

## Boas práticas importantes

* use sempre a chave pública no app cliente;
* nunca exponha `service_role` no frontend;
* configure RLS nas tabelas expostas;
* pense em autenticação e permissão como partes do projeto, não como detalhe final.

## Conclusão

Supabase é uma solução muito forte para projetos React Native porque reúne autenticação, banco e storage em um fluxo acessível. Para o curso, ele ajuda a aproximar bastante o aluno de uma stack real de aplicativo moderno.
