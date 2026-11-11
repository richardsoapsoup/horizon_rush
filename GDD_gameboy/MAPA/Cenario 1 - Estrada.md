# Mapas, Fases e Telas do Jogo

O jogo completo conta com **7 cenas no GB Studio**: **4 fases de corrida** em progressão climática (`160x1600` pixels / `20x200` tiles cada) e **3 telas de interface** (`160x144` pixels / `20x18` tiles cada).

---

## Progressão das 4 Fases de Corrida

Em todas as 4 fases:
- **Tamanho do Mapa:** `160x1600` pixels (`20` tiles de largura por `200` tiles de altura).
- **Colisões Laterais (Acostamento):**
  - Colunas `X = 0..4` (margem esquerda) = **Sólido** (impede o carro de sair da pista).
  - Colunas `X = 5..14` (asfalto central, `80px` de largura) = **Livre** (pista de corrida).
  - Colunas `X = 15..19` (margem direita) = **Sólido** (impede o carro de sair da pista).
- **Linha Branca de Chegada (*Trigger*):**
  - Desenhada no topo da pista (`Y = 24..31` px / Tile `Y = 2..3`, colunas `X = 5..14`) com um **Trigger** que avança automaticamente para a próxima fase (ou para a tela de **Vitória** ao concluir a Fase 4).

---

### Fase 1: Planícies Esmeralda (Estrada / Grama)
- **Cena no GB Studio:** `fase_1_grama` (`project/scenes/fase_1_grama/scene.gbsres`)
- **Tiles Únicos 8x8:** `37` tiles
- **Obstáculos:** `27` obstáculos distribuídos entre `Y = 18` e `Y = 180`
- **Próxima Cena ao Cruzar a Linha Branca:** `fase_2_deserto`
- **Sprite do Mapa:** `Sprites/Png/GBStudio/estrada_grama_gbs.png`
  ![[estrada_grama_gbs.png]]

---

### Fase 2: Cânion Escaldante (Deserto)
- **Cena no GB Studio:** `fase_2_deserto` (`project/scenes/fase_2_deserto/scene.gbsres`)
- **Tiles Únicos 8x8:** `67` tiles
- **Obstáculos:** `27` obstáculos em zigue-zague mais fechado
- **Próxima Cena ao Cruzar a Linha Branca:** `fase_3_mar`
- **Sprite do Mapa:** `Sprites/Png/GBStudio/estrada_deserto_gbs.png`
  ![[estrada_deserto_gbs.png]]

---

### Fase 3: Ponte Atlântica (Mar)
- **Cena no GB Studio:** `fase_3_mar` (`project/scenes/fase_3_mar/scene.gbsres`)
- **Tiles Únicos 8x8:** `64` tiles
- **Obstáculos:** `27` obstáculos com corredores duplos na pista costeira
- **Próxima Cena ao Cruzar a Linha Branca:** `fase_4_neve`
- **Sprite do Mapa:** `Sprites/Png/GBStudio/estrada_mar_gbs.png`
  ![[estrada_mar_gbs.png]]

---

### Fase 4: Pico Boreal (Neve)
- **Cena no GB Studio:** `fase_4_neve` (`project/scenes/fase_4_neve/scene.gbsres`)
- **Tiles Únicos 8x8:** `62` tiles
- **Obstáculos:** `27` obstáculos no desafio final de alta intensidade
- **Próxima Cena ao Cruzar a Linha Branca:** `vitoria` (Tela `WIN`)
- **Sprite do Mapa:** `Sprites/Png/GBStudio/estrada_neve_gbs.png`
  ![[estrada_neve_gbs.png]]

---

## Telas de Interface (`160x144` pixels)

### 1. Tela de Menu Inicial (`menu`)
- **Cena Inicial do Projeto:** Sim (`startSceneId` aponta para `menu`)
- **Música:** `Rulz_Intro.uge`
- **Ação:** O ator do jogador fica oculto (`EVENT_ACTOR_DEACTIVATE`). Pressionar **START** ou **A** toca um efeito sonoro de confirmação e carrega a **Fase 1 (`fase_1_grama`)**.
- **Sprite da Tela:** `Sprites/Png/GBStudio/menu_gbs.png`
  ![[menu_gbs.png]]

### 2. Tela de Vitória (`vitoria`)
- **Acionamento:** Ao cruzar a linha branca no final da **Fase 4 (`fase_4_neve`)**.
- **Música:** `Rulz_LightMood.uge`
- **Ação:** Pressionar **START**, **A** ou **B** retorna ao **Menu Inicial (`menu`)**.
- **Sprite da Tela:** `Sprites/Png/GBStudio/win_gbs.png`
  ![[win_gbs.png]]

### 3. Tela de Derrota / Game Over (`game_over`)
- **Acionamento:** Ao colidir com qualquer carro azul, carro verde, cone ou pedra em qualquer uma das 4 fases.
- **Música:** `Rulz_Pause_Underground.uge`
- **Ação:** Pressionar **START**, **A** ou **B** retorna ao **Menu Inicial (`menu`)**.
- **Sprite da Tela:** `Sprites/Png/GBStudio/lose_gbs.png`
  ![[lose_gbs.png]]
