---
description: >-
  Aprenda quais são os tipos de arquivos para disponibilizar seus aplicativos
  para o mundo inteiro
---

# Gerando o build do seu aplicativo

## Build e distribuição em React Native

### Introdução ao build

O processo de build em React Native envolve transformar o código JavaScript em um aplicativo nativo que possa ser executado em dispositivos Android e iOS. A principal ferramenta para o processo de build e distribuição em React Native é o Expo ou, para projetos nativos, o próprio React Native CLI com o Xcode (para iOS) e Android Studio (para Android).

### Tipos de builds e arquivos gerados

#### Builds de desenvolvimento

* **Android - APK Debug**: Para Android, o arquivo `.apk` é o pacote instalável que contém o aplicativo. Para fins de teste, um APK Debug pode ser gerado usando `react-native run-android`, permitindo que o app seja instalado diretamente em dispositivos Android.
* **iOS - Simulador e Dispositivos**: Para iOS, o build de desenvolvimento é gerado diretamente para o simulador ou dispositivo físico usando `react-native run-ios` ou pelo Xcode.

#### Builds de produção

* **APK (Android Package)**: É o formato padrão de instalação em Android. Um APK de produção é otimizado e preparado para ser enviado à Google Play Store.
* **AAB (Android App Bundle)**: É o formato recomendado pelo Google para publicação na Play Store. Um AAB inclui múltiplas versões do app (baseadas em especificações do dispositivo), reduzindo o tamanho do download final.
* **IPA**: O arquivo `.ipa` é o equivalente para iOS do APK. Para gerar um arquivo IPA em produção, precisamos de uma conta de desenvolvedor Apple e utilizar o Xcode para compilar o app em modo de distribuição.

### Gerando builds com Expo

Expo facilita o processo de criação de builds de produção para Android e iOS, sem a necessidade de um ambiente complexo de desenvolvimento. Vamos ver como gerar os arquivos APK, AAB e IPA.

**1 - Pré-requisitos para o Build**\
Antes de gerar o build, certifique-se de que:

* Sua aplicação Expo esteja funcionando e testada.
* Você tenha uma conta no Expo, pois os builds de produção são gerados nos servidores deles.
* Para iOS, tenha uma conta no Apple Developer Program.

**2 - Instalando o Expo CLI e Configurando o EAS**\
Expo Application Services (EAS) é o serviço que Expo oferece para builds na nuvem. Instale o `eas-cli`:

```bash
npm install -g eas-cli
```

Entre na sua conta Expo:

```bash
eas login
```

Depois, inicialize o EAS em seu projeto:

```bash
eas build:configure
```

Isso cria um arquivo `eas.json` na raiz do projeto, onde é possível configurar builds de desenvolvimento e produção.

**3 - Gerando Builds para Android**

**3.1 - Build APK para Testes Locais (Android)**

O APK é o formato padrão para Android, ideal para testes locais, mas não é recomendado para publicação na Play Store.

Para gerar um APK:

```bash
eas build -p android --profile preview
```

Após o build ser finalizado, você receberá um link para baixar o APK.

**3.2. Build AAB para Publicação (Android App Bundle)**

O Android App Bundle (AAB) é o formato recomendado pelo Google para publicação na Play Store, pois gera um app mais otimizado.

Para gerar o AAB:

```bash
eas build -p android --profile production
```

Este comando gera um AAB em modo de produção. Assim que o build for concluído, você receberá um link para baixar o arquivo e fazer o upload na Google Play Console.

**4 - Gerando Builds para iOS**

**4.1 - Preparando Certificados e Perfis de Provisionamento**

Para builds iOS, você precisará de uma conta no Apple Developer Program. Expo simplifica a criação e o gerenciamento dos certificados, mas é necessário fornecer as credenciais da Apple para a geração do IPA.

**4.2 - Build IPA para Publicação (iOS)**

Para gerar o build IPA para iOS:

```bash
eas build -p ios --profile production
```

Expo solicitará sua autorização para gerenciar os certificados e perfis de provisionamento. Após a conclusão do build, você receberá um link para baixar o arquivo IPA e fazer o upload no App Store Connect.



### Conclusão

Depois de criar as telas, integrar APIs, salvar dados e usar recursos do celular, chega um momento muito importante do projeto: colocar o aplicativo nas mãos de outras pessoas.

No desenvolvimento com Expo e React Native, uma das formas mais práticas de fazer isso é usando o **EAS Build**, serviço da Expo que gera o arquivo instalável do aplicativo sem exigir que todo o ambiente nativo esteja configurado na sua máquina.

Neste conteúdo, vamos focar no Android e aprender a gerar um **APK**, que pode ser instalado diretamente em um celular ou emulador para testes.

## APK ou AAB?

Antes de configurar o build, precisamos entender dois formatos muito comuns no Android:

* **APK (`.apk`)**: arquivo instalável diretamente em dispositivos Android. É ótimo para testes, validação com clientes, professores, colegas e distribuição interna.
* **AAB (`.aab`)**: formato recomendado para publicação na Google Play Store. Ele não é instalado diretamente no celular como um APK comum; a Google Play usa esse arquivo para gerar versões otimizadas para cada dispositivo.

Neste capítulo, vamos gerar um **APK de preview**, porque o objetivo é testar e compartilhar o app de forma simples.

## O que é o EAS?

EAS significa **Expo Application Services**. Ele reúne serviços da Expo para projetos React Native, como:

* geração de builds Android e iOS;
* gerenciamento de credenciais de assinatura;
* distribuição interna para testes;
* envio para lojas;
* atualizações remotas em projetos configurados para isso.

O serviço que vamos usar aqui é o **EAS Build**. Ele recebe o projeto, executa o processo de build na nuvem e gera o arquivo final do aplicativo.

## Pré-requisitos

Antes de gerar o APK, confirme se você tem:

* um projeto Expo funcionando;
* Node.js instalado;
* uma conta gratuita na Expo;
* acesso ao terminal na pasta do projeto;
* o app rodando localmente com `npx expo start`;
* o código salvo no Git, de preferência sem alterações pendentes importantes.

Também é importante testar o aplicativo antes do build. Se ele não funciona no desenvolvimento, provavelmente também não funcionará corretamente no APK.

## Instalando e acessando o EAS CLI

O EAS é usado pelo terminal através do pacote `eas-cli`.

Para instalar globalmente:

```bash
npm install -g eas-cli
```

Depois, faça login com sua conta Expo:

```bash
eas login
```

Para confirmar se o login funcionou:

```bash
eas whoami
```

Se o comando mostrar seu usuário da Expo, o ambiente está pronto para configurar o projeto.

## Configurando o projeto com EAS

Dentro da pasta do projeto, execute:

```bash
eas build:configure
```

Esse comando prepara o projeto para usar o EAS Build. Em muitos projetos Expo, ele cria ou ajusta arquivos como:

* `eas.json`;
* configurações de projeto da Expo;
* identificação do app para Android e iOS, quando necessário.

O arquivo mais importante neste momento é o `eas.json`, porque ele define os perfis de build.

## Entendendo o arquivo eas.json

O `eas.json` permite criar diferentes perfis de build. Cada perfil representa um tipo de versão do app.

Um exemplo comum:

```json
{
  "cli": {
    "version": ">= 13.0.0"
  },
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal"
    },
    "preview": {
      "distribution": "internal",
      "android": {
        "buildType": "apk"
      }
    },
    "production": {
      "android": {
        "buildType": "app-bundle"
      }
    }
  }
}
```

Neste exemplo:

* `development` gera uma versão para desenvolvimento, usada quando o app precisa de um cliente de desenvolvimento.
* `preview` gera um APK para instalação direta no Android.
* `production` gera um AAB, formato usado para publicação na Google Play.

O ponto principal para gerar APK está aqui:

```json
"android": {
  "buildType": "apk"
}
```

Essa configuração informa ao EAS que o build Android daquele perfil deve gerar um arquivo `.apk`.

## Gerando o APK

Com o EAS configurado, rode:

```bash
eas build -p android --profile preview
```

O parâmetro `-p android` indica que queremos gerar uma versão Android. O parâmetro `--profile preview` indica que o EAS deve usar o perfil `preview` definido no `eas.json`.

Durante o processo, o EAS pode perguntar sobre credenciais Android. Para um primeiro build, normalmente você pode deixar o próprio EAS gerar e gerenciar essas credenciais.

Ao final, o terminal mostrará um link para acompanhar o build no navegador. Quando o processo terminar, você poderá baixar o APK.

## Instalando o APK no celular

Depois que o build terminar, você pode instalar o APK de algumas formas.

### Instalando pelo link

A forma mais simples é:

1. Copiar o link do build gerado pelo EAS.
2. Abrir o link no celular Android.
3. Baixar o arquivo APK.
4. Autorizar a instalação de apps de fontes externas, se o Android solicitar.
5. Instalar e abrir o aplicativo.

Essa forma é útil quando você quer enviar o app para alguém testar.

### Instalando com adb

Se você usa Android Studio ou já tem o `adb` configurado, também pode instalar pelo terminal:

```bash
adb install caminho/do/aplicativo.apk
```

Caso o aplicativo já esteja instalado e você queira substituir a versão anterior:

```bash
adb install -r caminho/do/aplicativo.apk
```

## Rodando no emulador

O EAS também permite instalar builds recentes no emulador Android:

```bash
eas build:run -p android
```

Para instalar o build mais recente:

```bash
eas build:run -p android --latest
```

Esse comando lista os builds disponíveis e ajuda a instalar a versão escolhida no emulador.

## Variáveis de ambiente no Expo

Em muitos aplicativos, precisamos mudar configurações de acordo com o ambiente. Por exemplo:

* URL da API de homologação;
* URL da API de produção;
* flags para ativar ou desativar recursos;
* identificadores públicos de serviços externos.

No Expo, variáveis usadas dentro do código JavaScript devem começar com `EXPO_PUBLIC_`.

Crie um arquivo `.env` na raiz do projeto:

```env
EXPO_PUBLIC_API_URL=https://api.exemplo.com
EXPO_PUBLIC_APP_ENV=preview
```

No código, você pode acessar assim:

```tsx
const apiUrl = process.env.EXPO_PUBLIC_API_URL;

fetch(`${apiUrl}/produtos`);
```

As variáveis precisam ser acessadas diretamente com `process.env.NOME_DA_VARIAVEL`. Evite formatos dinâmicos, como `process.env["EXPO_PUBLIC_API_URL"]`, porque o Expo pode não substituir esse valor corretamente no bundle.

## Cuidado com informações sensíveis

Variáveis com prefixo `EXPO_PUBLIC_` ficam disponíveis no aplicativo gerado. Isso significa que elas podem ser vistas por quem analisar o app instalado.

Por isso, nunca coloque nestas variáveis:

* senhas;
* tokens privados;
* chaves secretas;
* credenciais de banco de dados;
* arquivos de serviço privados.

Use `EXPO_PUBLIC_` apenas para informações que podem estar no aplicativo, como a URL pública de uma API.

## Variáveis por perfil no eas.json

Além do arquivo `.env`, você pode definir variáveis dentro dos perfis do `eas.json`.

Exemplo:

```json
{
  "build": {
    "preview": {
      "distribution": "internal",
      "env": {
        "EXPO_PUBLIC_API_URL": "https://api-homologacao.exemplo.com",
        "EXPO_PUBLIC_APP_ENV": "preview"
      },
      "android": {
        "buildType": "apk"
      }
    },
    "production": {
      "env": {
        "EXPO_PUBLIC_API_URL": "https://api.exemplo.com",
        "EXPO_PUBLIC_APP_ENV": "production"
      },
      "android": {
        "buildType": "app-bundle"
      }
    }
  }
}
```

Com isso, o app pode usar uma API de homologação no APK de testes e uma API de produção no build final.

## Checklist antes de gerar o APK

Antes de executar o build, revise:

* O app roda localmente com `npx expo start`?
* O nome e o ícone do aplicativo estão corretos?
* As permissões usadas pelo app fazem sentido?
* A URL da API está configurada corretamente?
* O perfil `preview` está com `android.buildType` igual a `apk`?
* Não existem senhas ou tokens privados em variáveis `EXPO_PUBLIC_`?
* As principais telas foram testadas?

## Resumo

Neste conteúdo, aprendemos que o APK é ideal para testes e distribuição interna no Android. Também vimos como instalar o EAS CLI, configurar o projeto, criar perfis no `eas.json`, definir variáveis de ambiente e gerar o APK com:

```bash
eas build -p android --profile preview
```

Esse processo aproxima o projeto de uma publicação interna real, permitindo que outras pessoas instalem e testem o aplicativo fora do ambiente de desenvolvimento.Expo e EAS simplificam o processo de criação de builds de produção, possibilitando gerar APKs, AABs e IPAs sem necessidade de ambiente nativo complexo. Esses arquivos estão prontos para serem testados ou publicados nas lojas, permitindo que você disponibilize seu app para o público em qualquer lugar do mundo.
