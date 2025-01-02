# **[Guia Simplificado para Extrair L3 CDM com Android Studio](https://forum.videohelp.com/threads/408031-Dumping-Your-own-L3-CDM-with-Android-Studio)**

**Introdução**

Se você não tem um dispositivo Android ou não quer comprar um só para obter os dois arquivos necessários para descriptografar vídeos com DRM, não se preocupe! Você pode usar o Android Studio, disponível para Windows, Linux e Mac. Este tutorial é gratuito, mas você precisará de um computador com um bom processador e pelo menos 12 GB de RAM. Computadores mais lentos também funcionam, mas levará mais tempo para iniciar e usar o dispositivo virtual.

### **Passo 1: Instalar o Android Studio**

1. **Baixe e instale o Android Studio** do site oficial: [developer.android.com/studio](https://developer.android.com/studio).
2. Siga as instruções de instalação no assistente, utilizando as configurações recomendadas.

### **Passo 2: Criar um Dispositivo Android Virtual**

1. Abra o Android Studio e clique em **"Create Device"** para criar um dispositivo virtual.
2. Escolha um modelo de dispositivo, como o **"Pixel 6"**, e clique em **"Next"**.
3. Selecione uma versão do sistema operacional Android. O **Android Pie** é uma boa escolha e funciona bem com esse processo. Clique em **"Next"**.
4. Finalize clicando em **"Finish"**. O dispositivo virtual será criado, o que pode demorar alguns minutos.

### **Passo 3: Configurando o Emulador**

1. Após o dispositivo ser criado, ele aparecerá na lista. Clique para iniciá-lo, o que pode levar algum tempo.
2. Quando o dispositivo virtual estiver pronto, você terá um telefone virtual para prosseguir com os próximos passos.

### **Passo 4: Instalar Ferramentas Necessárias**

1. Abra o Prompt de Comando no Windows.
2. Instale o Frida e suas ferramentas, digitando os comandos:

   ```bash
   pip install frida
   pip install frida-tools
   ```

3. Baixe o **Frida Server para Android** em [GitHub - Frida Releases](https://github.com/frida/frida/releases). Coloque o arquivo baixado no diretório `C:\Users\seunome\AppData\Local\Android\Sdk\platform-tools`.

4. Certifique-se de que a versão do Frida Server corresponde à versão instalada via pip.

### **Passo 5: Conectar o Frida Server ao Dispositivo Virtual**

1. Abra o Prompt de Comando e verifique se o dispositivo está reconhecido pelo comando:

   ```bash
   adb.exe devices
   ```

2. Coloque o Frida Server no seu dispositivo virtual com o comando:

   ```bash
   adb.exe push frida-server-16.0.2-android-x86 /sdcard
   ```

3. Para configurar e executar o Frida Server, digite:

   ```bash
   adb.exe shell
   su
   mv /sdcard/frida-server-16.0.2-android-x86 /data/local/tmp
   chmod +x /data/local/tmp/frida-server-16.0.2-android-x86
   /data/local/tmp/frida-server-16.0.2-android-x86
   ```

   **Mantenha este terminal aberto.**

### **Passo 6: Baixar e Executar o Dumper**

1. Baixe o **Dumper** no GitHub: [Dumper](https://github.com/wvdumper/dumper).
2. Abra um novo Prompt de Comando, navegue até o diretório do Dumper usando `cd /...`, e execute:

   ```bash
   python dump_keys.py
   ```

3. Deixe este terminal aberto também.

### **Passo 7: Descriptografando o Vídeo**

1. No dispositivo virtual, abra o Google Chrome e acesse [Bitmovin DRM Demo](https://bitmovin.com/demos/drm) ou outro site com vídeos protegidos por DRM.
2. Enquanto o vídeo é reproduzido, o Dumper realizará seu trabalho em segundo plano.
3. Vá até o diretório do Dumper e você encontrará uma pasta chamada `private-keys` com dois arquivos:

   - `device_client_id_blob`
   - `device_private_key`

Esses arquivos são os que você precisa. Se precisar de mais L3 CDMs frescos, basta criar um novo dispositivo virtual e repetir o processo.