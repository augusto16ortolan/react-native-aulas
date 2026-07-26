---
description: >-
  Seguir boas práticas de nomenclatura e organização ajuda a escrever código
  mais limpo, previsível e fácil de manter.
---

# Padrões e boas práticas

<figure><img src="../.gitbook/assets/React Native (3).png" alt=""><figcaption></figcaption></figure>

Quando um projeto cresce, a maior dificuldade raramente é “fazer funcionar”. O desafio real passa a ser **entender, manter e evoluir** o código. Por isso, padrões de nomenclatura e pequenas boas práticas fazem tanta diferença.

## Convenções de nomenclatura

### `camelCase`

É o padrão mais comum para:

* variáveis;
* funções;
* propriedades;
* hooks personalizados.

```javascript
const nomeCompleto = "John Snow";
const dataNascimento = "1990-01-01";

function calcularTotal() {
  return 100;
}
```

### `PascalCase`

É o padrão ideal para:

* componentes React;
* classes;
* arquivos de componentes.

```javascript
function UserCard() {
  return null;
}

function ProductList() {
  return null;
}
```

### `snake_case`

É menos comum em JavaScript, mas pode aparecer:

* em nomes vindos de APIs;
* em bancos de dados;
* em integrações com back-end.

```javascript
const usuario_api = {
  first_name: "Ana",
  last_name: "Souza",
};
```

### `UPPER_SNAKE_CASE`

É usada para valores constantes e fixos.

```javascript
const API_URL = "https://api.exemplo.com";
const MAX_RETRIES = 3;
```

## Recomendações para este curso

Ao longo do material, vamos seguir este padrão:

* **variáveis e funções**: `camelCase`
* **componentes React Native**: `PascalCase`
* **constantes fixas**: `UPPER_SNAKE_CASE`
* **arquivos de componentes**: `PascalCase` ou nomes claros e consistentes com a estrutura do projeto

## Boas práticas importantes

### Use nomes significativos

```javascript
const totalDeVendas = 100;
const usuarioAtual = "John Snow";
```

Evite:

```javascript
const x = 100;
const u = "John Snow";
```

### Prefira `const` por padrão

Se o valor não precisa mudar, use `const`.

```javascript
const nomeProjeto = "Tarefas App";
let contador = 0;
```

Isso reduz efeitos colaterais e deixa a intenção mais clara.

### Evite abreviações desnecessárias

```javascript
const quantidadeDeProdutos = 50;
```

Evite:

```javascript
const qtdProd = 50;
```

### Mantenha um idioma consistente

Escolha um idioma para nomes de variáveis e funções e siga esse padrão no projeto inteiro.

Se a turma preferir português, tudo bem. O importante é não misturar sem motivo:

```javascript
const usuarioLogado = true;
const userName = "Ana";
```

Esse tipo de mistura dificulta a leitura.

### Separe responsabilidade

Mesmo em exemplos pequenos, tente evitar arquivos “gigantes” com tudo junto. Em apps React Native, é comum separar:

* componentes;
* telas;
* serviços;
* contextos;
* utilitários.

### Escreva pensando em quem vai ler depois

Esse “alguém” pode ser:

* você daqui a duas semanas;
* um colega;
* um avaliador;
* um futuro time de manutenção.

Código limpo não é código “bonito”. É código que outra pessoa consegue entender sem sofrimento.

## Conclusão

Boas práticas não servem para deixar o código “mais formal”. Elas servem para diminuir erros, acelerar manutenção e tornar o projeto sustentável. Em aplicativos, isso pesa ainda mais, porque a lógica cresce rápido e envolve interface, navegação, estado e integração com serviços externos.
