---
description: A comunicação eficiente entre cliente e servidor
---

# APIs e Métodos/Retornos HTTP

<figure><img src="../.gitbook/assets/7.jpg" alt=""><figcaption></figcaption></figure>

As APIs (Application Programming Interfaces) são conjuntos de definições e protocolos que permitem que diferentes aplicações se comuniquem entre si. Em um contexto web, as APIs são frequentemente usadas para facilitar a interação entre um cliente (como um navegador ou aplicativo móvel) e um servidor. Para gerenciar essa comunicação, são utilizados métodos HTTP, que determinam a ação a ser executada no servidor, e códigos de status HTTP, que informam o resultado dessa ação.

### Exemplos de APIs legais para desenvolvedores

1. Advide Slipe API ([https://api.adviceslip.com/](https://api.adviceslip.com/))
2. Pokémon API ([https://pokeapi.co/](https://pokeapi.co/))
3. The Dog API ([https://www.thedogapi.com/](https://www.thedogapi.com/))
4. The Cat API ([https://thecatapi.com/](https://thecatapi.com/))
5. Deck of Cards API ([https://www.deckofcardsapi.com/](https://www.deckofcardsapi.com/))
6. The Open Movie Database ([https://www.omdbapi.com/](https://www.omdbapi.com/))
7. Fun Translations API ([https://api.funtranslations.com/](https://api.funtranslations.com/))
8. Random User Data API ([https://randomuser.me/](https://randomuser.me/))
9. Fake Store API ([https://fakestoreapi.com/](https://fakestoreapi.com/))
10. ViaCEP API ([https://viacep.com.br/](https://viacep.com.br/))

Link de um GitHub que contém muitos exemplos interessantes de APIs para utilizar em projetos: [https://github.com/public-apis/public-apis](https://github.com/public-apis/public-apis)

### Métodos HTTP

Métodos HTTP (Hypertext Transfer Protocol) são os comandos usados para interagir com recursos em um servidor web. Cada método tem um propósito específico e define a ação desejada em relação a um recurso. Aqui estão os métodos HTTP mais comuns:

1. **GET**: Solicita a representação de um recurso. É utilizado para obter dados de um servidor sem modificar o estado do recurso. É o método mais utilizado para leitura de dados.
2. **POST**: Envia dados para o servidor para criar um novo recurso. O servidor processa os dados enviados e pode retornar uma resposta com o status da operação ou o recurso criado.
3. **PUT**: Atualiza ou substitui um recurso existente no servidor. Envia os dados completos do recurso para o servidor, que substitui o recurso atual pelos novos dados fornecidos.
4. **DELETE**: Remove um recurso especificado do servidor. É usado para deletar recursos existentes.
5. **PATCH**: Atualiza parcialmente um recurso existente. Envia apenas os dados que precisam ser alterados, e não o recurso completo.

### Códigos de Status/Retorno HTTP

Códigos de status HTTP são respostas enviadas pelo servidor para indicar o resultado de uma solicitação feita pelo cliente. Eles ajudam a entender o sucesso ou falha da requisição e fornecem informações adicionais sobre o estado da resposta.

1. **2xx Sucesso**: Indica que a solicitação foi bem-sucedida.
   * **200 OK**: A solicitação foi bem-sucedida e o servidor retornou os dados solicitados.
   * **201 Created**: A solicitação foi bem-sucedida e um novo recurso foi criado.
2. **4xx Erro do Cliente**: Indica que houve um problema com a solicitação do cliente.
   * **400 Bad Request**: A solicitação é inválida ou malformada.
   * **401 Unauthorized**: O cliente não está autenticado.
   * **404 Not Found**: O recurso solicitado não foi encontrado.
3. **5xx Erro do Servidor**: Indica que houve um problema no servidor ao processar a solicitação.
   * **500 Internal Server Error**: Ocorreu um erro genérico no servidor.
   * **503 Service Unavailable**: O servidor está temporariamente indisponível.

### Exemplos

Aqui estão exemplos de como você pode usar `async` e `await` em JavaScript para fazer chamadas a uma API fictícia. Vamos usar a API fictícia `https://api.exemplo.com` para ilustrar isso.

#### Obtendo dados com GET

```javascript
// Função assíncrona para obter usuários
async function obterUsuarios() {
    try {
        // Envia uma solicitação GET para a API
        let resposta = await fetch('https://api.exemplo.com/usuarios');
        
        // Verifica se a resposta foi bem-sucedida
        if (!resposta.ok) {
            throw new Error(`Erro na resposta: ${resposta.statusText}`);
        }
        
        // Converte a resposta em JSON
        let dados = await resposta.json();
        
        // Exibe os dados no console
        console.log(dados);
    } catch (erro) {
        // Trata qualquer erro que possa ocorrer
        console.error('Erro ao obter usuários:', erro);
    }
}

// Chama a função para obter usuários
obterUsuarios();
```

#### Enviando dados com POST

Neste exemplo, vamos enviar dados para criar um novo usuário.

```javascript
// Função assíncrona para criar um usuário
async function criarUsuario(nome, email) {
    try {
        // Dados do novo usuário
        let novoUsuario = {
            nome: nome,
            email: email
        };

        // Envia uma solicitação POST para a API
        let resposta = await fetch('https://api.exemplo.com/usuarios', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(novoUsuario)
        });

        // Verifica se a resposta foi bem-sucedida
        if (!resposta.ok) {
            throw new Error(`Erro na resposta: ${resposta.statusText}`);
        }

        // Converte a resposta em JSON
        let dados = await resposta.json();

        // Exibe o novo usuário no console
        console.log('Usuário criado:', dados);
    } catch (erro) {
        // Trata qualquer erro que possa ocorrer
        console.error('Erro ao criar usuário:', erro);
    }
}

// Chama a função para criar um usuário
criarUsuario('João Silva', 'joao.silva@exemplo.com');
```

#### Atualizando dados com PUT

Neste exemplo, vamos atualizar as informações de um usuário existente.

```javascript
// Função assíncrona para atualizar um usuário
async function atualizarUsuario(id, nome, email) {
    try {
        // Dados atualizados do usuário
        let usuarioAtualizado = {
            nome: nome,
            email: email
        };

        // Envia uma solicitação PUT para a API
        let resposta = await fetch(`https://api.exemplo.com/usuarios/${id}`, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(usuarioAtualizado)
        });

        // Verifica se a resposta foi bem-sucedida
        if (!resposta.ok) {
            throw new Error(`Erro na resposta: ${resposta.statusText}`);
        }

        // Converte a resposta em JSON
        let dados = await resposta.json();

        // Exibe o usuário atualizado no console
        console.log('Usuário atualizado:', dados);
    } catch (erro) {
        // Trata qualquer erro que possa ocorrer
        console.error('Erro ao atualizar usuário:', erro);
    }
}

// Chama a função para atualizar um usuário
atualizarUsuario(1, 'João Silva', 'joao.silva@novoexemplo.com');
```

#### Removendo dados com DELETE

Neste exemplo, vamos remover um usuário existente.

```javascript
// Função assíncrona para remover um usuário
async function removerUsuario(id) {
    try {
        // Envia uma solicitação DELETE para a API
        let resposta = await fetch(`https://api.exemplo.com/usuarios/${id}`, {
            method: 'DELETE'
        });

        // Verifica se a resposta foi bem-sucedida
        if (!resposta.ok) {
            throw new Error(`Erro na resposta: ${resposta.statusText}`);
        }

        // Exibe uma mensagem de sucesso
        console.log('Usuário removido com sucesso.');
    } catch (erro) {
        // Trata qualquer erro que possa ocorrer
        console.error('Erro ao remover usuário:', erro);
    }
}

// Chama a função para remover um usuário
removerUsuario(1);
```

Esses exemplos mostram como você pode usar `async` e `await` para trabalhar com APIs em Javascript, facilitando a leitura e manutenção do código assíncrono.

### Conclusão

Entender APIs, métodos HTTP e códigos de status é essencial para desenvolver aplicações web que interajam eficazmente com servidores. APIs facilitam a comunicação entre clientes e servidores, enquanto métodos HTTP (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`) definem as ações a serem realizadas com os dados. Os códigos de status HTTP fornecem feedback sobre o sucesso ou falha das solicitações.

Os exemplos demonstram como usar `async` e `await` para fazer requisições assíncronas a uma API fictícia, ilustrando a obtenção, criação, atualização e remoção de dados. Esse conhecimento permite construir aplicações robustas e responsivas, garantindo uma comunicação clara e eficiente entre o front-end e o back-end.
