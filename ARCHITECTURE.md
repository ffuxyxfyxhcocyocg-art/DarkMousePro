# Arquitetura — Dark Mouse Pro

```
[Teclado/Mouse/Gamepad]
        │
        ▼
 /dev/input  ──getevent -q──► RawInput (thread) ──► MapEngine (HandlerThread)
                                                          │
                                                          ▼
                                              TouchInjector (IInputManager
                                              injectInputEvent via Shizuku)
                                                          │
                                                          ▼
                                              Toques multitoque no jogo

UI (MainActivity + Screens) ──► ProfileStore / GameStore / Backup
        │
        ▼
 MappingService (FGS specialUse)
   - bolha flutuante + painel
   - EditorOverlay
   - RawInput + MapEngine
   - autoSwitch (dumpsys window via Shizuku)
```

## Componentes
| Classe | Papel |
|--------|--------|
| TouchInjector | injectInputEvent multitoque |
| RawInput | parse getevent |
| MapEngine | teclas/eixos → toques do perfil |
| MappingService | FGS, overlay, ciclo de vida |
| EditorOverlay | edição visual sobre o jogo |
| ProfileStore | JSON em SharedPreferences |
| ShizukuMgr | estado, spawn, exec |
| BackupManager | backup com SHA-256 |

## Limites Android
- Sem Shizuku/root: sem getevent privilegiado nem inject
- Mouse físico ainda gera eventos no sistema
- Jogos podem filtrar toque injetado
