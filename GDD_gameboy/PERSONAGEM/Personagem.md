# O Carro do Jogador — "Relâmpago Rubro" (*Red Viper*)

## Papel no Jogo
O único veículo controlado pelo jogador durante as 4 etapas da **Copa dos Quatro Climas**. Trata-se do protótipo esportivo vermelho **Relâmpago Rubro** (*Red Viper*), pilotado por **Alex "Faísca"**, com visão superior (*top-down*).

Por conta da falha mecânica na largada (parte central da [[Historia]]), o carro avança **automaticamente para cima** em velocidade constante ao longo da rodovia, cabendo ao jogador controlar o deslocamento lateral (**Esquerda / Direita**) para desviar dos obstáculos.

---

## Visual e Sprite
- **Sprite:** `Sprites/Png/Carro.png` (e versão de máscara do GB Studio em `Sprites/Png/GBStudio/carro_gbs.png`)
  ![[Carro.png]]

### Especificações Técnicas do Sprite no GB Studio
- **Dimensões:** `16x16` pixels (composto por 2 *hardware sprites* de `8x16` lado a lado).
- **Cor de Transparência GB Studio:** Fundo `#65FF00` no asset de compilação.
- **Paleta Exclusiva GBC (`pal_carro_vermelho.gbsres` — Slot 0 / `OBP0`):**
  - **Tom Claro (Faróis / Para-brisa):** `#C8C8C8` (Cinza claro / Prata)
  - **Tom Médio (Lataria Principal):** `#D80000` (Vermelho vibrante)
  - **Tom Escuro (Pneus / Contorno):** `#181818` (Preto / Grafite escuro)
- **Orientação Fixa (`fixed`):** O sprite utiliza `animationType: "fixed"` no GB Studio para manter o carro sempre apontando para cima na estrada, mesmo quando o jogador desliza (*strafe*) para a esquerda ou direita.

---

## Atributos e Física no GB Studio
- **Posição Inicial em Cada Fase:** Tile `X = 9`, `Y = 195` (centralizado na base da estrada de `20x200` tiles).
- **Velocidade de Movimento (`moveSpeed`):** `2` (deslocamento ágil e responsivo tanto na subida automática quanto nas trocas de faixa).
- **Caixa de Colisão (*Hitbox* Generosa):**
  - `boundsX: 2`, `boundsY: -2`, `boundsWidth: 12`, `boundsHeight: 11` (menor que os `16x16` pixels totais do sprite para evitar mortes injustas de raspão).
- **Vidas / Resistência:** Estilo arcade clássico de **morte súbita** (*1 Hit = Game Over*). Qualquer colisão com um obstáculo do `Collision Group 1` aciona um som de batida e leva para a tela de `Game Over` (`LOSE`).
