# Integrando Back-end com Front-end

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Para que um aplicativo React Native possa realizar operações CRUD e interagir com dados armazenados em um servidor, é necessário estabelecer uma comunicação entre o app (frontend) e o backend. Essa integração é feita por meio de APIs (Application Programming Interfaces) que possibilitam a troca de dados entre o cliente (o app) e o servidor.

### API

Em nosso contexto, uma API permite que um aplicativo React Native envie e receba dados de um servidor. As APIs são como "pontes" que conectam seu aplicativo a serviços externos, sejam eles para autenticação, bancos de dados, processamento de pagamentos, ou qualquer outro tipo de funcionalidade.

### Métodos HTTP e operações CRUD

A comunicação entre o React Native e o backend ocorre por meio de requisições HTTP. Aqui estão os métodos HTTP mais comuns e como eles se relacionam com as operações CRUD:

* **POST**: Usado para **criar** novos dados no servidor.
* **GET**: Usado para **ler** ou **recuperar** dados.
* **PUT/PATCH**: Usado para **atualizar** dados existentes.
* **DELETE**: Usado para **excluir** dados do servidor.

### Estrutura básica de uma requisição HTTP

Quando seu aplicativo React Native precisa se comunicar com o backend, ele envia uma **requisição HTTP**. A estrutura básica de uma requisição inclui:

* **URL**: O endereço para onde a requisição será enviada.
* **Método HTTP**: Especifica a ação desejada (GET, POST, PUT, DELETE).
* **Cabeçalhos (Headers)**: Informações adicionais sobre a requisição, como autenticação e tipo de conteúdo.
* **Corpo (Body)**: Dados que são enviados junto com a requisição (usado principalmente em POST e PUT).

### Configurações necessárias para integrar com um back-end

Para integrar um aplicativo React Native com um backend, é necessário ter um backend configurado que seja capaz de responder a requisições HTTP. Aqui estão alguns componentes típicos de um backend:

* **Servidor Web**: Responsável por receber e responder às requisições HTTP (ex.: Express.js, Spring Boot, Django).
* **Banco de Dados**: Onde os dados são armazenados (ex.: PostgreSQL, MongoDB, MySQL).
* **APIs RESTful**: Endpoints que permitem que o app interaja com o backend (ex.: `/api/usuarios`, `/api/tarefas`).

### Ferramentas para integração em React Native

Existem diversas ferramentas e bibliotecas que facilitam a integração com um backend em aplicativos React Native:

* **fetch API**: Disponível nativamente no JavaScript, é usada para fazer requisições HTTP.
* **axios**: Uma biblioteca popular para fazer requisições HTTP que oferece uma sintaxe mais amigável e recursos adicionais, como interceptadores e manipulação de erros.
* **React Query**: Para gerenciar dados assíncronos, fazer cache e sincronizar com um backend.

### Segurança na comunicação

Ao integrar um aplicativo com um backend, é essencial garantir que a comunicação seja segura. Algumas práticas recomendadas incluem:

* **HTTPS**: Use sempre `https://` para garantir que os dados sejam transmitidos de forma segura.
* **Tokens de Autenticação**: Use mecanismos de autenticação, como JWT (JSON Web Tokens), para validar usuários e proteger recursos.
* **Validação e Sanitização**: Certifique-se de que os dados recebidos e enviados sejam validados e sanitisados para evitar ataques como SQL Injection e XSS.

### Fluxo de trabalho típico para integração

1. **Usuário Interage com o App**: O usuário faz uma ação no aplicativo (ex.: clica em um botão para adicionar uma nova tarefa).
2. **O App Envia uma Requisição para o Backend**: Uma requisição HTTP é enviada ao servidor com os detalhes da nova tarefa.
3. **Backend Processa a Requisição**: O servidor recebe a requisição, processa os dados e interage com o banco de dados para armazenar a nova tarefa.
4. **Backend Envia uma Resposta**: O servidor responde ao app com uma confirmação de sucesso ou uma mensagem de erro.
5. **O App Atualiza a Interface**: Com base na resposta do backend, o aplicativo atualiza a interface do usuário para refletir a nova informação.

### Conclusão

A integração de aplicativos React Native com um backend é um processo essencial para criar aplicativos que sejam dinâmicos e possam interagir com dados em tempo real. Com uma compreensão clara de como as requisições HTTP funcionam, como configurar um backend e quais ferramentas usar, os alunos estarão prontos para criar aplicativos poderosos e conectados.
