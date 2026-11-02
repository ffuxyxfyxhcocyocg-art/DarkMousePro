# Dark Mouse Pro 1.1.0

Mapeador de teclado e mouse para Android (Kotlin, Views nativas, minSdk 31, targetSdk 35).

## Gerar o APK

**Sem PC: GitHub Actions**
1. Crie um repositório no GitHub e suba esta pasta.
2. Aba *Actions* > *Build APK* > espere ficar verde.
3. Baixe o artefato **DarkMousePro-apk** (debug e release; os dois instalam).

**Com Android Studio / SDK:** `gradle assembleRelease` (APK em `app/build/outputs/apk/release/`).

## Como usar
1. Instale o **Shizuku**, ligue a depuração sem fio, pareie e inicie o serviço. Abra a Central Shizuku do app e autorize.
2. Ative "Sobrepor a outros apps" para o Dark Mouse Pro.
3. Jogos > Adicionar jogo (lista todos os apps do telefone).
4. Ferramentas > Mapeamentos: crie um layout FPS/MOBA/Livre para o jogo, toque em **Editar layout** (o editor abre por cima do jogo) e depois em **Iniciar**.
5. Tecla de pausa do mapeamento (padrão F8) libera o mouse/teclado para o menu do jogo.

## Como funciona (e limites)
- Leitura de teclado/mouse/gamepad: `getevent` executado pelo Shizuku (usuário shell). Só leitura.
- Toques: `IInputManager.injectInputEvent` pelo Binder do Shizuku (multitoque real). Não mexe na memória do jogo nem injeta código.
- O ponteiro/cliques do mouse continuam chegando ao Android; jogos que tratam mouse nativamente podem reagir duas vezes. Não há como bloquear isso sem root.
- Alguns jogos ignoram ou tratam diferente toque injetado. Só testando no seu aparelho.
- O layout é guardado em frações da tela: edite na mesma orientação em que vai jogar.
- Não há mira automática, cheat, nem macro com repetição automática (macro = até 12 toques, sem loop).

## Estado de verificação
- O Kotlin passa no typecheck (kotlinc contra android.jar 34 + stubs do Shizuku/HiddenApiBypass).
- Patches FASE 1–5 (auditoria, robustez Shizuku/getevent, suavização de mouse, import/export de perfil, diag expandido).
Build Gradle completo e testes em aparelho: usar GitHub Actions ou Android Studio. Runtime ainda não validado neste ambiente.
