---
description: >-
  Um fluxo simples para escolher ou capturar imagens e enviar arquivos para o
  Supabase Storage.
---

# Fazendo upload de imagens

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

Upload de imagens é um recurso muito comum em aplicativos:

* foto de perfil;
* imagens de produto;
* comprovantes;
* anexos de formulário.

Neste exemplo, vamos usar:

* **Expo Image Picker**
* **Expo FileSystem**
* **Supabase Storage**

## Fluxo geral

1. o usuário escolhe uma imagem da galeria ou tira uma foto;
2. o app recebe o `uri` local do arquivo;
3. o arquivo é convertido para envio;
4. a imagem é enviada para um bucket no Supabase;
5. o app recebe a URL e pode exibir a imagem.

## Instalação

```bash
npx expo install expo-image-picker expo-file-system
npx expo install @supabase/supabase-js @react-native-async-storage/async-storage react-native-url-polyfill
npm install base64-arraybuffer
```

## Variáveis de ambiente

No arquivo `.env`:

```env
EXPO_PUBLIC_SUPABASE_URL=https://seu-projeto.supabase.co
EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY=sua_chave_publica_aqui
```

## Preparando o bucket

No Supabase:

* crie um bucket chamado `images`;
* para uma primeira prática, você pode deixá-lo público;
* em projetos reais, pense com cuidado entre bucket público e privado.

## Cliente Supabase

```jsx
import "react-native-url-polyfill/auto";
import AsyncStorage from "@react-native-async-storage/async-storage";
import { createClient } from "@supabase/supabase-js";

const supabase = createClient(
  process.env.EXPO_PUBLIC_SUPABASE_URL,
  process.env.EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY,
  {
    auth: {
      storage: AsyncStorage,
      autoRefreshToken: true,
      persistSession: true,
      detectSessionInUrl: false,
    },
  }
);

export default supabase;
```

## Exemplo completo

```jsx
import "react-native-url-polyfill/auto";
import { useState } from "react";
import { View, Text, StyleSheet, Button, Image, Alert } from "react-native";
import * as ImagePicker from "expo-image-picker";
import * as FileSystem from "expo-file-system";
import { decode } from "base64-arraybuffer";
import AsyncStorage from "@react-native-async-storage/async-storage";
import { createClient } from "@supabase/supabase-js";

const supabase = createClient(
  process.env.EXPO_PUBLIC_SUPABASE_URL,
  process.env.EXPO_PUBLIC_SUPABASE_PUBLISHABLE_KEY,
  {
    auth: {
      storage: AsyncStorage,
      autoRefreshToken: true,
      persistSession: true,
      detectSessionInUrl: false,
    },
  }
);

export default function UploadImage() {
  const [localUri, setLocalUri] = useState(null);
  const [publicUrl, setPublicUrl] = useState(null);
  const [uploading, setUploading] = useState(false);

  async function uploadToSupabase(uri) {
    try {
      setUploading(true);

      const base64 = await FileSystem.readAsStringAsync(uri, {
        encoding: FileSystem.EncodingType.Base64,
      });

      const arrayBuffer = decode(base64);
      const fileExt = uri.split(".").pop()?.toLowerCase() || "jpg";
      const fileName = `${Date.now()}.${fileExt}`;
      const filePath = `uploads/${fileName}`;

      const contentType =
        fileExt === "png"
          ? "image/png"
          : fileExt === "webp"
          ? "image/webp"
          : "image/jpeg";

      const { error } = await supabase.storage
        .from("images")
        .upload(filePath, arrayBuffer, {
          contentType,
          upsert: false,
        });

      if (error) {
        console.error(error);
        Alert.alert("Erro", "Não foi possível enviar a imagem.");
        return;
      }

      const { data } = supabase.storage.from("images").getPublicUrl(filePath);
      setPublicUrl(data.publicUrl);
      Alert.alert("Sucesso", "Imagem enviada!");
    } catch (error) {
      console.error(error);
      Alert.alert("Erro", "Algo deu errado no upload.");
    } finally {
      setUploading(false);
    }
  }

  async function pickFromGallery() {
    const permission =
      await ImagePicker.requestMediaLibraryPermissionsAsync();

    if (!permission.granted) {
      Alert.alert("Permissão necessária", "Permita acesso à galeria.");
      return;
    }

    const result = await ImagePicker.launchImageLibraryAsync({
      mediaTypes: ["images"],
      allowsEditing: true,
      quality: 1,
    });

    if (result.canceled) return;

    const uri = result.assets[0].uri;
    setLocalUri(uri);
    setPublicUrl(null);
    await uploadToSupabase(uri);
  }

  async function takePhoto() {
    const permission = await ImagePicker.requestCameraPermissionsAsync();

    if (!permission.granted) {
      Alert.alert("Permissão necessária", "Permita acesso à câmera.");
      return;
    }

    const result = await ImagePicker.launchCameraAsync({
      allowsEditing: true,
      quality: 1,
    });

    if (result.canceled) return;

    const uri = result.assets[0].uri;
    setLocalUri(uri);
    setPublicUrl(null);
    await uploadToSupabase(uri);
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Upload de Imagens</Text>

      <View style={styles.buttons}>
        <Button
          title={uploading ? "Enviando..." : "Escolher da Galeria"}
          onPress={pickFromGallery}
          disabled={uploading}
        />
        <Button
          title={uploading ? "Enviando..." : "Tirar Foto"}
          onPress={takePhoto}
          disabled={uploading}
        />
      </View>

      {localUri && (
        <>
          <Text style={styles.label}>Prévia local:</Text>
          <Image source={{ uri: localUri }} style={styles.image} />
        </>
      )}

      {publicUrl && (
        <>
          <Text style={styles.label}>URL pública:</Text>
          <Text selectable style={styles.url}>
            {publicUrl}
          </Text>

          <Text style={styles.label}>Imagem armazenada:</Text>
          <Image source={{ uri: publicUrl }} style={styles.image} />
        </>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    gap: 12,
  },
  title: {
    fontSize: 20,
    fontWeight: "700",
  },
  buttons: {
    gap: 10,
  },
  label: {
    marginTop: 8,
    fontWeight: "600",
  },
  image: {
    width: "100%",
    height: 220,
    borderRadius: 10,
    backgroundColor: "#eee",
  },
  url: {
    fontSize: 12,
  },
});
```

## Observações importantes

* `EXPO_PUBLIC_` não deve guardar segredos privados.
* Em apps reais, muitas vezes você vai salvar no banco o caminho do arquivo ou a URL retornada.
* Buckets privados exigem outro fluxo, como URL assinada.

## Conclusão

Esse fluxo já resolve a maior parte dos cenários iniciais de upload em aplicativos React Native. Ele conecta recurso do dispositivo, manipulação de arquivo e armazenamento em nuvem de um jeito bem próximo do uso real.
