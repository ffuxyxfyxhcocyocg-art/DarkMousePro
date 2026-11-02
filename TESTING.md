# Testes

## Automatizados
Pasta `app/src/test` vazia. Não há testes unitários executados.

## Manuais recomendados (aparelho + Shizuku)
1. Instalar Shizuku, parear, autorizar o app
2. Conceder sobreposição
3. Criar perfil FPS para um jogo, editar layout, iniciar
4. WASD → joystick; mouse → câmera; clique → botão
5. Pausar (tecla do perfil / F10), confirmar toques liberados
6. Desconectar Shizuku → mapeamento deve parar sem teclas presas
7. Import/export de perfil JSON
8. Calibração: alterar smooth/curve e sentir diferença na mira
9. autoSwitch: abrir dois jogos com perfis e alternar

## Resultados neste ambiente
Nenhum teste de runtime executado (sem emulador/dispositivo/SDK).


## Unit (esqueleto)
`app/src/test/java/com/darkmouse/pro/KeysTest.kt` — nomes de teclas e SHA estável.
Requer `./gradlew test` com SDK.
