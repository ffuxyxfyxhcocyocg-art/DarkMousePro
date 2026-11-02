# Dark Mouse Pro 1.1.0 — Entrega

Data: 2026-11-02  
Base: projeto existente no ZIP original (não reescrito do zero).

## 1. Código-fonte
Pasta: `DarkMousePro/` (Kotlin, Views, minSdk 31, targetSdk 35).

Arquivos principais (`app/src/main/java/com/darkmouse/pro/`):

| Arquivo | Linhas (aprox.) | Papel |
|---------|-----------------|--------|
| MainActivity.kt | 845 | UI, navegação, home, diag, Shizuku |
| Screens.kt | 563 | Jogos, ferramentas, config, calibração, backup |
| Service.kt | 509 | FGS, bolha, editor, watcher, binder dead |
| Input.kt | 478 | TouchInjector, RawInput, MapEngine |
| Editor.kt | 438 | Editor visual overlay |
| Model.kt | 356 | Keys, Control, Profile, ProfileStore |
| Ui.kt | 113 | Tema preto/vermelho |
| Backup.kt | 104 | Backup/restore SHA-256 + perfil avulso |
| ShizukuMgr.kt | 103 | Estado/spawn/exec Shizuku |
| Data.kt | 89 | Apps, GameStore, Devices |

## 2. Funcionalidades implementadas / preservadas

### Já existiam (preservadas e usadas)
- Leitura de entrada via `getevent` (Shizuku)
- Injeção multitoque via `IInputManager.injectInputEvent`
- Joystick WASD, botões, câmera (mouse), macros curtas
- Editor visual sobre o jogo (mover, tamanho, opacidade, teclas)
- Perfis por pacote, templates FPS/MOBA/Livre
- Painel flutuante, pause por tecla
- Lista de jogos, dispositivos, Central Shizuku
- Backup com SHA-256

### Adicionadas / reforçadas nesta sessão (1.1.0)
- ProfileStore atômico + `recoverIfNeeded`
- Import/export de **perfil avulso** (JSON)
- Undo do editor com throttle + autosave
- Mouse: deadzone, suavização, curva (+ UI em Calibração)
- RawInput/MapEngine: teclas presas, destroyForcibly, retry
- Service: InputDeviceListener, binder dead Shizuku, watcher com limite de falhas
- Home: status de sobreposição e mapeamento
- Diagnóstico expandido
- Pro+ tab informativa
- Debounce na busca de apps
- Teste unitário esqueleto `KeysTest`
- Documentação completa (ARCHITECTURE, BUILD, TESTING, ROADMAP, DELIVERY, PHASE*)

## 3. Erros encontrados e corrigidos

| Problema | Correção |
|----------|----------|
| Write de perfis não atômico | `all_bak` + `commit` + recover |
| getevent/processo sem limpeza | `destroyForcibly` + retry |
| Teclas/toques presos no fail | `heldKeys` + `release` no onFail/binder dead |
| Overlay sem atalho | Intent `ACTION_MANAGE_OVERLAY_PERMISSION` |
| spawn Shizuku genérico | Checks de binder/permissão + log |
| Câmera “crua” | smooth / curve / mouseDeadzone |
| Undo excessivo no arraste | Throttle 350 ms + force no UP |
| Import só backup envelope | Aceita perfil JSON simples |
| Watcher autoSwitch frágil | Contador de falhas, para após 3 |
| Versão desatualizada na UI | Strings 1.1.0 / versionCode 2 |

## 4. Testes
- **Runtime em device:** não executado (sem SDK/emulador neste ambiente).
- **Unit:** `KeysTest` preparado; rodar com `./gradlew test` onde houver SDK.
- **Build APK:** não gerado aqui; usar GitHub Actions ou Android Studio (ver BUILD.md).

## 5. Limitações conhecidas
- Shizuku (ou root/ADB shell) obrigatório para mapear.
- Eventos do mouse físico ainda chegam ao Android (possível duplicidade em jogos com mouse nativo).
- Alguns jogos filtram ou ignoram toque injetado.
- AIDL `IShellService` declarado mas não usado no runtime atual.
- Release assinado com keystore **debug** no Gradle atual (trocar antes de distribuição séria).
- autoSwitch usa `dumpsys window` a cada 2,5 s (custo baixo, mas depende do Shizuku).

## 6. Instalação e uso
1. Instalar Shizuku, iniciar serviço (depuração sem fio), autorizar o app.
2. Conceder “Sobrepor a outros apps”.
3. Jogos → adicionar jogo → Ferramentas → Mapeamentos → template → Editar layout → Iniciar.
4. Bolha flutuante: pausar / editar / parar. Tecla de pause do perfil (padrão F8) também pausa.

## 7. Gerar APK
```text
# GitHub Actions
Push → Actions → "Build APK" → baixar artefato

# Local
./gradlew assembleDebug assembleRelease
# app/build/outputs/apk/...
```
Detalhes: BUILD.md

## 8. APK neste ambiente
**Não disponível.** Não há Android SDK/sandbox de build Android. O artefato entregue é o **código-fonte** + docs.

## 9. Plano do que ainda falta
Ver ROADMAP.md. Prioridades sugeridas:
1. Compilar e validar em 2–3 aparelhos reais
2. Keystore de release
3. Mais testes unitários (ProfileStore, Backup round-trip)
4. Preview de layout
5. Schema versionado nos perfis

## 10. Zips de trabalho
- `DarkMousePro_FASE1_6.zip` — snapshot final desta sessão
