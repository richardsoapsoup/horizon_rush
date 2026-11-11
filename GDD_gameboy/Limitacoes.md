# Limitações Técnicas (Game Boy Color / GB Studio 4.3.2)

Este documento detalha as limitações reais de hardware do **Game Boy Color (GBC)** e da engine **GB Studio 4.3.2**, bem como todas as adaptações técnicas aplicadas nos assets e na programação do jogo.

---

## 1. Resolução e Mapas de Background
- **Resolução da Tela do GBC:** `160x144` pixels (`20x18` tiles de `8x8` pixels).
- **Telas de Interface (`menu.png`, `win.png`, `lose.png`):** Exatamente `160x144` pixels (`20x18` tiles).
- **Mapas das 4 Fases (`estrada_grama.png`, `estrada_deserto.png`, `estrada_mar.png`, `estrada_neve.png`):**
  - As imagens originais (`320x3200` pixels com pixels dobrados 2x2) foram redimensionadas na proporção exata para **`160x1600` pixels** (`20x200` tiles de `8x8`), respeitando o limite máximo de altura do GB Studio (`<= 2040px`) e a largura exata da tela (`160px`).
  - No topo de cada estrada (`Y = 24..31` px, `X = 40..119` px), foi adicionada a **Linha Branca de Chegada** onde fica o *Trigger* de transição de fase.

---

## 2. Limite de Tiles Únicos em VRAM (Backgrounds)
- **Regra do GB Studio / GBC:** Um background não pode ultrapassar **192 tiles únicos de 8x8 pixels** (ou 384 no modo GBC estendido). Além disso, cada tile individual de `8x8` pixels pode conter no máximo **4 cores**.
- **Otimização Aplicada nos Backgrounds:**
  - Todos os 7 backgrounds passaram por quantização automática por bloco `8x8` (máximo de 4 cores por tile e até 8 paletas GBC por cena):
    - `estrada_grama.png`: **37 tiles únicos**
    - `estrada_deserto.png`: **67 tiles únicos**
    - `estrada_mar.png`: **64 tiles únicos**
    - `estrada_neve.png`: **62 tiles únicos**
    - `menu.png`: **46 tiles únicos**
    - `win.png`: **48 tiles únicos**
    - `lose.png`: **59 tiles únicos**

---

## 3. Sprites e Paletas do Game Boy Color
- **Regra do GB Studio para Sprites:**
  - Todo sprite deve usar a cor exata **`#65FF00`** como fundo transparente.
  - Os pixels visíveis do sprite no arquivo `.png` devem ser pintados com as 3 cores de máscara do GB Studio, que o compilador mapeia para a paleta GBC atribuída ao sprite:
    - `#07FF00` -> **Cor Clara (Light — `colors[0]`)**
    - `#00FF00` -> **Cor Média (Mid — `colors[1]`)**
    - `#007F00` -> **Cor Escura (Dark — `colors[3]`)** *(Nota: `colors[2]` na estrutura de paleta `.gbsres` é ignorado pelo compilador de sprites do GB Studio)*.
- **Paletas Customizadas Criadas (`project/palettes/`):**
  - **Slot 0 (`pal_carro_vermelho`):** `["C8C8C8", "D80000", "900000", "181818"]` (Carro do Jogador)
  - **Slot 1 (`pal_carro_azul`):** `["F8F038", "4070C0", "204080", "181818"]` (Carro Azul)
  - **Slot 2 (`pal_carro_verde`):** `["F8F038", "68C030", "388018", "181818"]` (Carro Verde)
  - **Slot 3 (`pal_cone`):** `["F8F8F8", "E86820", "A04010", "202038"]` (Cone)
  - **Slot 4 (`pal_pedra`):** `["A0A0A0", "606060", "404040", "080808"]` (Pedra)

---

## 4. Limites de Entidades (Atores e Hardware Sprites)
- **Máximo por Scanline:** `10` sprites de `8x16` por linha horizontal (`scanline`). Como cada ator `16x16` usa `2` sprites de `8x16`, posicionar no máximo **2 obstáculos na mesma altura Y** + **1 jogador** consome no máximo `6` sprites por linha (evitando 100% de cintilação/*flickering*).
- **Máximo de Atores por Cena:** Cada fase utiliza **27 atores de obstáculos** (dentro do limite seguro do GB Studio de até 30 atores por cena).

---

## 5. Áudio (`hUGEDriver` / `.uge` v6)
- O chip de som do Game Boy possui **4 canais simultâneos**:
  1. **Duty 1 (Onda Quadrada c/ Sweep):** Melodia principal e arpejo de introdução.
  2. **Duty 2 (Onda Quadrada):** Contra-arpejo de harmonia e eco estéreo.
  3. **Wave (Onda Programável de 32 amostras de 4 bits):** Linha de baixo (*Sawtooth*).
  4. **Noise (Gerador de Ruído LFSR):** Percussão (*Kick*, *Snare* e *Hi-Hat*) e efeitos sonoros de colisão (`crash`).
- O arquivo `topgear1.mid` foi convertido diretamente para `assets/music/topgear1.uge` (formato binário UGE v6 com `33` ordens de sequência e `132` *patterns* de `64` linhas a `6` *ticks* por linha).
