# Controles do Jogo

O esquema de controles foi projetado para resposta imediata no Game Boy Color, já que o **Relâmpago Rubro** acelera automaticamente pela estrada.

## Durante as Fases de Corrida (Fases 1 a 4)

| Botão do Game Boy | Ação no Jogo |
| :--- | :--- |
| **D-Pad Esquerda** | Desloca o carro para a esquerda na pista (`dx = -1, dy = -1`), desviando de obstáculos enquanto continua subindo. |
| **D-Pad Direita** | Desloca o carro para a direita na pista (`dx = +1, dy = -1`), desviando de obstáculos enquanto continua subindo. |
| **Avanço Vertical** | **Automático.** O carro avança sozinho continuamente rumo à linha branca no topo da estrada. |

---

## Nas Telas de Menu, Vitória e Game Over

| Tela | Botões Aceitos | Ação |
| :--- | :--- | :--- |
| **Menu Inicial (`MENU`)** | **START** ou **A** | Inicia a corrida na **Fase 1: Planícies Esmeralda (Grama)**. |
| **Tela de Vitória (`WIN`)** | **START**, **A** ou **B** | Retorna para o **Menu Inicial**. |
| **Tela de Derrota (`LOSE`)** | **START**, **A** ou **B** | Retorna para o **Menu Inicial** para tentar novamente. |

---

## Comportamento Visual da Direção (*Strafe*)
O carro mantém o sprite voltado para cima (`animationType: "fixed"`), deslizando lateralmente entre as faixas da estrada com *hitbox* reduzida (`12x11` pixels), garantindo leitura visual clara em alta velocidade no Game Boy Color.
