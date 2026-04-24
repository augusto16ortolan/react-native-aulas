---
description: >-
  Um fluxo simples com duas formas de obter a imagem (galeria ou câmera) e fazer
  upload no Storage na nuvem.
---

# Fazendo upload de imagens

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

### Como funciona

1. **Você pega uma imagem**
   * **Galeria**: o usuário escolhe uma foto já existente
   * **Câmera**: o usuário tira uma foto na hora
2. O Expo te devolve um **`uri` local** (ex.: `file://...`).
3. Para enviar ao Storage do Supabase no React Native, um jeito bem “tranquilo” é:
   * ler o arquivo em **base64** (`expo-file-system`)
   * converter para **ArrayBuffer**
   * usar `supabase.storage.from("bucket").upload(...)`
4. Depois do upload, você pode:
   * pegar uma **URL pública** (se o bucket for público)
   * ou usar URL assinada (mais seguro, mas aqui vamos manter simples)

### Preparação rápida

#### 1) Instale as libs

```
npx expo install expo-image-picker expo-file-systemnpm i @supabase/supabase-js base64-arraybuffer react-native-url-polyfill
```

#### 2) Variáveis de ambiente (Expo)

No `.env`:

```
EXPO_PUBLIC_SUPABASE_URL="SUA_URL_AQUI"
EXPO_PUBLIC_SUPABASE_ANON_KEY="SUA_ANON_KEY_AQUI"
```

#### 3) Storage no Supabase

* Crie um bucket chamado **`images`**
* Para o exemplo ficar bem simples, deixe o bucket como **public** (assim `getPublicUrl` funciona direto)

### Código completo (bem simples) — Galeria + Câmera + Upload

```jsx
import "react-native-url-polyfill/auto";
import React, { useState } from "react";
import { View, Text, StyleSheet, Button, Image, Alert } from "react-native";
import * as ImagePicker from "expo-image-picker";
import * as FileSystem from "expo-file-system";
import { decode } from "base64-arraybuffer";
import { createClient } from "@supabase/supabase-js";

const supabaseUrl = process.env.EXPO_PUBLIC_SUPABASE_URL;
const supabaseAnonKey = process.env.EXPO_PUBLIC_SUPABASE_ANON_KEY;

const supabase = createClient(supabaseUrl, supabaseAnonKey);

export default function UploadImage() {
  const [localUri, setLocalUri] = useState(null);
  const [publicUrl, setPublicUrl] = useState(null);
  const [uploading, setUploading] = useState(false);

  async function uploadToSupabase(uri) {
    try {
      setUploading(true);

      // 1) Lê a imagem em base64
      const base64 = await FileSystem.readAsStringAsync(uri, {
        encoding: FileSystem.EncodingType.Base64,
      });

      // 2) Base64 -> ArrayBuffer
      const arrayBuffer = decode(base64);

      // 3) Define nome/caminho do arquivo
      const fileExt = uri.split(".").pop()?.toLowerCase() || "jpg";
      const fileName = `${Date.now()}.${fileExt}`;
      const filePath = `uploads/${fileName}`;

      // 4) Define contentType simples
      const contentType =
        fileExt === "png"
          ? "image/png"
          : fileExt === "webp"
          ? "image/webp"
          : "image/jpeg";

      // 5) Faz upload no bucket "images"
      const { error } = await supabase.storage
        .from("images")
        .upload(filePath, arrayBuffer, {
          contentType,
          upsert: true,
        });

      if (error) {
        console.log(error);
        Alert.alert("Erro", "Não foi possível enviar a imagem.");
        return;
      }

      // 6) URL pública (bucket precisa ser public)
      const { data } = supabase.storage.from("images").getPublicUrl(filePath);
      setPublicUrl(data.publicUrl);

      Alert.alert("Sucesso", "Imagem enviada!");
    } catch (e) {
      console.error(e);
      Alert.alert("Erro", "Algo deu errado no upload.");
    } finally {
      setUploading(false);
    }
  }

  async function pickFromGallery() {
    const permission = await ImagePicker.requestMediaLibraryPermissionsAsync();
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

          <Text style={styles.label}>Imagem na nuvem:</Text>
          <Image source={{ uri: publicUrl }} style={styles.image} />
        </>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20, gap: 12 },
  title: { fontSize: 20, fontWeight: "700" },
  buttons: { gap: 10 },
  label: { marginTop: 8, fontWeight: "600" },
  image: {
    width: "100%",
    height: 220,
    borderRadius: 10,
    backgroundColor: "#eee",
  },
  url: { fontSize: 12 },
});
```

### Conclusão

Com Expo, você consegue implementar upload de imagens de forma bem direta: **(1) escolher da galeria ou tirar foto**, **(2) pegar o `uri`**, **(3) fazer upload para o Storage do Supabase** e **(4) exibir a imagem pela URL**. Esse padrão já resolve a maior parte dos apps iniciais e é fácil de evoluir depois (bucket privado, URL assinada, salvar caminho no banco, etc.).
