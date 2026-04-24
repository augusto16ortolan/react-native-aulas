---
description: >-
  Aprenda quais são os tipos de arquivos para disponibilizar seus aplicativos
  para o mundo inteiro
---

# Gerando o build do seu aplicativo

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

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

Expo e EAS simplificam o processo de criação de builds de produção, possibilitando gerar APKs, AABs e IPAs sem necessidade de ambiente nativo complexo. Esses arquivos estão prontos para serem testados ou publicados nas lojas, permitindo que você disponibilize seu app para o público em qualquer lugar do mundo.
