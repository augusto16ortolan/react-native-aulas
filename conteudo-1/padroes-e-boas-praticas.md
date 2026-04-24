---
description: >-
  Seguir boas práticas de nomenclatura e estilo ajuda a criar um código mais
  limpo e compreensível. Isso não só facilita a manutenção e a colaboração, mas
  também melhora a eficiência do desenvolvimento.
---

# Padrões e boas práticas

<figure><img src="../.gitbook/assets/React Native (3).png" alt=""><figcaption></figcaption></figure>

## Nomenclaturas

As convenções de nomenclatura são importantes para manter o código legível e consistente. Em Javascript, existem várias convenções que ajudam a distinguir diferentes tipos de identificadores, como variáveis, funções, classes e constantes.

### **Camel Case**

A primeira palavra começa com letra minúscula e cada palavra subsequente começa com letra maiúscula. É a convenção mais comum para variáveis e funções.

```javascript
nomeCompleto = "Jhon Snow";
dataNascimento = "01/01/1990";
quantidadeVenda = 10;
```

### **Pascal Case**

Todas as palavras começam com letra maiúscula, incluindo a primeira. É frequentemente usada para classes e construtores.

```javascript
NomeCompleto = "Jhon Snow";
DataNascimento = "01/01/1990";
QuantidadeVenda = 10;
```

### **Snake Case**

Todas as letras são minúsculas e as palavras são separadas por underscores (`_`). É menos comum em Javascript, mas ainda pode ser visto em algumas bases de código.

```javascript
nome_completo = "Jhon Snow";
data_nascimento = "01/01/1990";
quantidade_venda = 10;
```

### **Upper Snake Case**

Uma variação da snake case onde todas as letras são maiúsculas. É frequentemente usada para constantes que têm valores fixos.

```javascript
NOME_COMPLETO = "Jhon Snow";
DATA_NASCIMENTO = "01/01/1990";
QUANTIDADE_VENDA = 10;
```

### **Recomendações em JavaScript**

* **Camel Case**: Usado para variáveis e funções. Exemplo: `nomeCompleto`, `calcularImposto()`.
* **Pascal Case**: Usado para classes e construtores. Exemplo: `Pessoa`, `Produto`.
* **Snake Case**: Menos comum em JavaScript, mas pode ser usado em contextos específicos ou para manter compatibilidade com outras linguagens ou padrões.
* **Upper Snake Case**: Usado para constantes que não devem ser alteradas. Exemplo: `MAX_TEMPERATURA`.

## Boas práticas

Adotar boas práticas ao escrever código JavaScript ajuda a garantir que o código seja claro, legível e fácil de manter. Aqui estão algumas diretrizes importantes:

### Nomes significativos e descritivos

Utilize nomes que claramente reflitam o propósito e o uso das variáveis, funções e outros identificadores.

#### Bom exemplo:

```javascript
let totalDeVendas = 100;
let usuarioAtual = "Jhon Snow";
```

#### Mau exemplo:

```javascript
let x = 100;
let nm = "Jhon Snow";
```

### Consistência

Mantenha uma convenção de nomenclatura e estilo de código consistente em todo o projeto. Isso melhora a legibilidade e facilita a colaboração em equipe.\
Escolha uma convenção (como camelCase para variáveis e funções, PascalCase para classes) e a siga rigorosamente.

### Evite abreviações

Abreviações podem ser confusas e dificultar a compreensão do código. Use nomes completos a menos que a abreviação seja amplamente compreendida.

#### Bom exemplo:

```javascript
let quantidadeDeProdutos = 50;
```

#### Mau exemplo:

```javascript
let qtProd = 50;
```

### Defina um idioma

Use um idioma consistente ao longo do código. Isso é especialmente importante em equipes internacionais para evitar confusões.

## Conclusão

Ao adotar nomes significativos e descritivos, manter consistência em todo o projeto e evitar abreviações confusas, você não apenas melhora a legibilidade do código, mas também facilita a colaboração e a manutenção a longo prazo. Seguir esses princípios não apenas reforça a qualidade do código, mas também promove uma cultura de excelência e profissionalismo entre desenvolvedores. Lembre-se, boas práticas na programação são a base para criar soluções robustas e de alta qualidade que podem evoluir e prosperar no futuro.
