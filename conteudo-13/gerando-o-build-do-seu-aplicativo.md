---
description: >-
  Aprenda a gerar builds Android com Expo e EAS para testes e preparação de
  publicação.
---

# Gerando o build do seu aplicativo

Depois de desenvolver e testar o app localmente, chega a hora de transformá-lo em um arquivo instalável.

No ecossistema Expo atual, o caminho mais comum para isso é o **EAS Build**.

## Formatos principais no Android

### APK

O `.apk` pode ser instalado diretamente em celular ou emulador. É muito útil para:

* testes internos;
* validação com colegas;
* apresentação de projeto;
* distribuição fora da loja.

### AAB

O `.aab` é o formato recomendado para publicação na Google Play. Ele não é instalado diretamente no aparelho como um APK comum.

## O que é o EAS

**EAS** significa **Expo Application Services**. É o conjunto de serviços da Expo para:

* builds;
* credenciais;
* distribuição;
* submissão para lojas.

## Pré-requisitos

Antes de gerar o build:

* o projeto precisa abrir com `npx expo start`;
* você precisa ter conta na Expo;
* o app deve ter nome, ícone e configuração mínima revisados;
* é importante checar variáveis de ambiente e permissões.

## Instalando o EAS CLI

```bash
npm install -g eas-cli
```

Depois:

```bash
eas login
```

Você pode confirmar o login com:

```bash
eas whoami
```

## Configurando o projeto

Na raiz do projeto:

```bash
eas build:configure
```

Esse comando cria ou ajusta o arquivo `eas.json`.

## Exemplo de `eas.json`

```json
{
  "cli": {
    "version": ">= 13.0.0"
  },
  "build": {
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

Nesse exemplo:

* `preview` gera APK;
* `production` gera AAB.

## Gerando um APK

```bash
eas build -p android --profile preview
```

Esse comando envia o projeto para build na nuvem e gera um APK para testes.

## Gerando um AAB

```bash
eas build -p android --profile production
```

Esse é o formato mais comum para publicação na Google Play.

## Instalando o APK

Depois do build concluído, você pode:

1. abrir o link do build no celular;
2. baixar o APK;
3. instalar o aplicativo;
4. testar fora do ambiente de desenvolvimento.

Se você tiver `adb`, também pode instalar pelo terminal:

```bash
adb install caminho/do/app.apk
```

Para substituir uma instalação existente:

```bash
adb install -r caminho/do/app.apk
```

## Variáveis de ambiente no Expo

No Expo, variáveis usadas no código cliente devem usar `EXPO_PUBLIC_`.

Exemplo:

```env
EXPO_PUBLIC_API_URL=https://api.exemplo.com
EXPO_PUBLIC_APP_ENV=preview
```

Uso no código:

```jsx
const apiUrl = process.env.EXPO_PUBLIC_API_URL;
```

Nunca coloque segredos privados nessas variáveis, porque elas ficam embutidas no app final.

## Checklist antes do build

* o app abre com `npx expo start`?
* as principais telas foram testadas?
* o nome, ícone e splash screen estão corretos?
* as permissões fazem sentido?
* as URLs de API estão corretas?
* não há segredos privados em `EXPO_PUBLIC_`?

## Conclusão

Gerar o build é o passo que transforma o projeto em algo instalável por outras pessoas. Com Expo e EAS, esse processo fica bem mais acessível e prepara o caminho para testes externos e publicação.
