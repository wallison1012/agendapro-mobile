# 📱 AgendaPro Mobile App

Aplicativo Android para as donas de salão acessarem o AgendaPro.

## ✨ Funcionalidades

- 🎨 Interface nativa com tema AgendaPro (Rose Gold)
- 🔄 Splash screen animada
- 📲 Acesso direto ao painel via WebView
- 💾 Suporte a navegação offline (cache)
- 📱 Otimizado para celulares

## 🚀 Como Gerar o APK

### Opção 1: Usando Android Studio (Recomendado)

1. **Instale o Android Studio**:
   - Baixe em: https://developer.android.com/studio
   - Instale com SDK Android 34

2. **Abra o projeto**:
   ```bash
   # No Windows
   cd C:\caminho\para\mobile-app
   
   # No Mac/Linux
   cd /caminho/para/mobile-app
   ```

3. **Sincronize o Capacitor**:
   ```bash
   npm install
   npx cap sync
   ```

4. **Abra no Android Studio**:
   ```bash
   npx cap open android
   ```

5. **Gere o APK**:
   - No Android Studio: Build → Build Bundle(s) / APK(s) → Build APK(s)
   - O APK será gerado em: `android/app/build/outputs/apk/debug/app-debug.apk`

### Opção 2: Linha de Comando (Linux/Mac)

```bash
# Requisitos: Android SDK instalado e ANDROID_HOME configurado

# 1. Entre na pasta
cd mobile-app

# 2. Instale dependências
npm install

# 3. Sincronize com Android
npx cap sync

# 4. Build do APK
cd android
./gradlew assembleDebug

# APK gerado em:
# android/app/build/outputs/apk/debug/app-debug.apk
```

## 📋 Estrutura do Projeto

```
mobile-app/
├── android/              # Projeto Android nativo (gerado)
├── www/                  # Arquivos web
│   └── index.html       # Splash screen
├── resources/            # Ícones e splash
├── capacitor.config.json # Configuração
└── package.json
```

## 🎨 Personalização

### Alterar URL do painel:
Edite `capacitor.config.json`:
```json
{
  "server": {
    "url": "https://seu-dominio.com"
  }
}
```

Depois execute:
```bash
npx cap sync
```

### Alterar cores:
Edite `www/index.html` e modifique as variáveis CSS:
```css
--primary: #C9A96E;      /* Rose Gold */
--secondary: #8B3A52;    /* Vinho */
--accent: #F2D4D7;       /* Rosa Nude */
```

### Alterar ícone:
Substitua `resources/icon.svg` e execute:
```bash
npx capacitor-assets generate
```

## 📲 Instalação no Celular

### Método 1: APK Debug (Testes)
```bash
adb install android/app/build/outputs/apk/debug/app-debug.apk
```

### Método 2: APK Release (Distribuição)
```bash
# Gerar keystore (primeira vez)
keytool -genkey -v -keystore agenda-pro.keystore -alias agendapro -keyalg RSA -keysize 2048 -validity 10000

# Build release
cd android
./gradlew assembleRelease

# Assinar APK
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore agenda-pro.keystore app/build/outputs/apk/release/app-release-unsigned.apk agendapro

# Otimizar
zipalign -v 4 app/build/outputs/apk/release/app-release-unsigned.apk app-release.apk
```

## 🔧 Requisitos

- Node.js 16+
- Android SDK 34
- Java 8+
- Gradle 8.0+

## 🐛 Solução de Problemas

### Erro: "Capacitor not found"
```bash
npm install -g @capacitor/cli
```

### Erro: "ANDROID_HOME not set"
```bash
# Linux/Mac
export ANDROID_HOME=$HOME/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools

# Windows (no CMD)
set ANDROID_HOME=C:\Users\SeuUsuario\AppData\Local\Android\Sdk
set PATH=%PATH%;%ANDROID_HOME%\tools;%ANDROID_HOME%\platform-tools
```

### Erro: "Gradle sync failed"
```bash
# Limpar cache
cd android
./gradlew clean
cd ..
npx cap sync
```

## 📄 Licença

Parte do sistema AgendaPro.
