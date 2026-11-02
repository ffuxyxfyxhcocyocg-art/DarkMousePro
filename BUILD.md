# Build

## Requisitos
- JDK 17+
- Android SDK 35
- Gradle 8.10+ (wrapper no projeto)

## GitHub Actions (recomendado sem PC)
1. Push desta pasta para um repositório
2. Actions → *Build APK*
3. Baixar artefato `DarkMousePro-apk`

## Local
```bash
./gradlew assembleDebug assembleRelease
# APKs em app/build/outputs/apk/
```

Release está assinada com a keystore **debug** (instalável direto; troque para keystore própria antes de distribuir).

## Este ambiente
Sem Android SDK — APK não foi gerado aqui.
