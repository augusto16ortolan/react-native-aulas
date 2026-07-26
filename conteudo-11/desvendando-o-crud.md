---
description: >-
  Aprenda os fundamentos de CRUD e como essas operações aparecem no dia a dia
  de aplicativos móveis.
---

# Desvendando o CRUD

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

CRUD é o conjunto das quatro operações mais comuns em sistemas que manipulam dados:

1. **Create**: criar
2. **Read**: ler
3. **Update**: atualizar
4. **Delete**: excluir

Quase todo aplicativo com dados faz isso o tempo todo.

## CRUD no contexto de um app

Imagine um aplicativo de tarefas:

* criar uma nova tarefa;
* listar as tarefas já cadastradas;
* editar o título ou marcar como concluída;
* remover uma tarefa que não faz mais sentido.

Isso é CRUD.

## Onde o CRUD acontece

No mobile, essas operações podem acontecer de duas formas:

* **localmente**: com armazenamento no dispositivo, como `@react-native-async-storage/async-storage`;
* **remotamente**: via API ou serviço como Supabase.

Na prática, a maioria dos apps reais mistura os dois cenários em algum nível.

## CRUD e métodos HTTP

Quando o app conversa com um backend, o CRUD costuma aparecer assim:

* **Create** → `POST`
* **Read** → `GET`
* **Update** → `PUT` ou `PATCH`
* **Delete** → `DELETE`

## Exemplo mental simples

Se o usuário cadastrar uma nova tarefa:

* a tela envia um `POST`;
* o servidor salva;
* o app atualiza a lista exibida.

Se o usuário excluir:

* a tela envia um `DELETE`;
* o servidor remove;
* a interface deixa de mostrar aquele item.

## Por que CRUD é tão importante?

Porque ele organiza o pensamento do projeto. Quando você olha para uma funcionalidade e pergunta:

* o que precisa ser criado?
* o que precisa ser listado?
* o que o usuário poderá editar?
* o que poderá ser removido?

você já está estruturando uma parte importante do aplicativo.

## Conclusão

CRUD é um dos pilares do desenvolvimento de software e aparece naturalmente em projetos React Native. Entender essas quatro operações deixa muito mais claro como construir telas, integrar APIs e organizar o fluxo de dados do aplicativo.
