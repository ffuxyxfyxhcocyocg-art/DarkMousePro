# Changelog

## 1.1.0 — 2026-11-02
### Confiabilidade
- ProfileStore: gravação com backup `all_bak` + recuperação automática de JSON corrompido
- RawInput: `destroyForcibly`, reinício após falha, release de toques no fail
- MapEngine: rastreio de teclas físicas (`heldKeys`), release completo no pause/fail
- Service: listener de dispositivos, binder dead do Shizuku, watcher de auto-switch com limite de falhas
- Overlay: atalho para settings quando permissão falta

### Mouse / câmera
- Zona morta, suavização EMA e curva de resposta (ajustáveis em Calibração)
- Backup/restore dos novos prefs

### Perfis
- Import de perfil avulso (JSON simples)
- Export do menu grava JSON de perfil (não só envelope de backup)
- Undo do editor com throttle + snapshot no fim do arraste

### UI / diagnóstico
- Home: status de sobreposição e mapeamento
- Pro+ tab com resumo real + atalhos
- Versão 1.1.0 nas settings
- Picker: debounce na busca
- Editor: autosave após edições
- Home: status de sobreposição e mapeamento
- Diagnóstico: overlay, mapeamento, contagem de perfis

### Notas
- Sem teste em aparelho neste ambiente (sem Android SDK)
- AIDL IShellService permanece declarado mas não usado em runtime
