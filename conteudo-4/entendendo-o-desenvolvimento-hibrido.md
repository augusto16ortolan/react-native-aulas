---
description: >-
  Descubra o conceito de desenvolvimento híbrido e como ele permite criar
  aplicativos que funcionam em múltiplas plataformas usando uma única base de
  código.
---

# Entendendo o desenvolvimento híbrido

<figure><img src="../.gitbook/assets/React Native (4).png" alt=""><figcaption></figcaption></figure>

O desenvolvimento híbrido com React Native é uma abordagem que permite criar aplicativos para dispositivos móveis (como smartphones e tablets) que funcionam tanto no sistema Android quanto no iOS com um único código-fonte.

### Código compartilhado

Com React Native, você escreve o código do aplicativo em Javascript, uma linguagem de programação muito popular para desenvolvimento web.\
Esse código pode ser usado para criar aplicativos que funcionam em diferentes plataformas (Android e iOS), ao invés de ter que escrever dois códigos diferentes, um para cada plataforma.

### Componentes nativos

React Native usa componentes nativos, ou seja, elementos que são próprios do sistema Android ou iOS (como botões, textos, imagens, etc.). Isso garante que o aplicativo tenha uma aparência e desempenho similares aos aplicativos desenvolvidos nativamente para essas plataformas.

### Reutilização de código

Grande parte do código que você escreve pode ser reutilizada para ambas as plataformas, o que economiza tempo e esforço no desenvolvimento. Apenas algumas partes específicas, como integração com funcionalidades específicas do dispositivo (GPS, câmera, etc.), podem precisar de adaptações.

### Desenvolvimento e atualização rápida

Como o código é compartilhado e escrito em uma linguagem familiar para desenvolvedores web, o desenvolvimento de aplicativos pode ser mais rápido e as atualizações podem ser feitas de forma mais eficiente.

### Benefícios

**Economia de Tempo e Custo**: Não é necessário ter equipes separadas para desenvolver aplicativos para Android e iOS. Um único desenvolvedor ou equipe pode criar um aplicativo que funcione em ambas as plataformas.

**Performance Similar ao Nativo**: Apesar de ser um framework híbrido, React Native oferece uma performance muito próxima aos aplicativos desenvolvidos nativamente.

**Grande Comunidade e Suporte**: React Native é mantido pelo Facebook e tem uma grande comunidade de desenvolvedores, o que significa que há muito suporte e recursos disponíveis.

### Arquitetura do React Native

<figure><img src="../.gitbook/assets/ChatGPT Image 2 de fev. de 2026, 22_21_36.png" alt=""><figcaption></figcaption></figure>

A **Nova Arquitetura do React Native** é uma atualização profunda dos “bastidores” do framework para melhorar **performance**, **responsividade da UI** e **integração com código nativo**. Ela foi criada para substituir o modelo antigo, que dependia muito do “Bridge” (uma ponte de comunicação que adicionava overhead e latência em várias situações).

#### O que muda na ideia geral

Em vez de ficar trocando mensagens serializadas pelo Bridge, a Nova Arquitetura se apoia em um núcleo mais moderno (com partes em C++) e numa integração mais direta entre **JavaScript ↔ nativo**, reduzindo custos de comunicação e facilitando recursos mais avançados.

### Componentes principais

#### JSI (JavaScript Interface)

A **JSI** é a base que permite o JavaScript “conversar” com o lado nativo de forma mais direta e eficiente (em vez de depender do Bridge antigo).

#### Turbo Native Modules (TurboModules)

Os **Turbo Native Modules** são a nova forma de criar módulos nativos (aquilo que você chama do JS, mas executa no Android/iOS). Eles usam um **arquivo de especificação tipada** (TypeScript/Flow) e um gerador de código para criar as interfaces necessárias.

**Benefícios que costumam ser citados:**

* integração mais sólida (menos “gambiarras” de bridge)
* possibilidade de inicialização mais eficiente (ex.: carregar quando precisa)
* contratos mais claros entre JS e nativo (por causa da tipagem)

#### Codegen (geração de código)

O **Codegen** é a ferramenta que lê a especificação (TS/Flow) e gera as “pontes”/interfaces usadas pelos TurboModules (e também por componentes de UI do novo sistema).

#### Fabric (novo renderer de UI)

O **Fabric** é o novo “motor” de renderização da interface. Em termos simples: ele moderniza como o React Native desenha e atualiza componentes na tela, ajudando a deixar a UI mais fluida e com melhor coordenação entre JS e nativo.

#### Bridgeless Mode

O **Bridgeless** é um passo adicional dentro da Nova Arquitetura: ele remove dependências restantes do Bridge legado e melhora a confiabilidade do runtime.

### Conclusão

O desenvolvimento híbrido com React Native é uma forma eficiente e prática de criar aplicativos móveis de alta qualidade que funcionam em múltiplas plataformas, economizando tempo e recursos e facilitando a manutenção e atualização dos aplicativos.
