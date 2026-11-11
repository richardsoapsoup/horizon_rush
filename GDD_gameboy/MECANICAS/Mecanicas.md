# Mecânicas Principais e Implementação no GB Studio

## 1. Avanço Automático e Direção Lateral
- **Posição de Largada:** Em cada uma das 4 fases, o carro vermelho inicia na base da rodovia (`X = 9, Y = 195`) apontando para o norte (`up`).
- **Subida Automática (`EVENT_LOOP`):**
  - Após iniciar a música da fase e aguardar `0.2s`, o script principal da cena entra em um `EVENT_LOOP` infinito que move o jogador continuamente `1` tile para cima (`EVENT_ACTOR_MOVE_RELATIVE`, `dy = -1`, `collideWith: ["walls", "actors"]`).
- **Direção Esquerda / Direita sem Travar a Subida (`EVENT_SET_INPUT_SCRIPT`):**
  - Como o motor Top-Down padrão do GB Studio bloquearia os controles manuais durante um `EVENT_ACTOR_MOVE_RELATIVE`, os botões **Esquerda (`left`)** e **Direita (`right`)** possuem *scripts* anexados (`persist: true`) que movem o jogador na diagonal superior-esquerda (`dx = -1, dy = -1`) ou superior-direita (`dx = +1, dy = -1`).
  - Isso garante que o carro continue avançando para cima na estrada enquanto muda de faixa suavemente para a esquerda ou para a direita.

---

## 2. Barreiras da Estrada (Limites Laterais)
- Cada mapa de estrada tem `20` tiles de largura (`160px`):
  - As 5 colunas da esquerda (`X = 0..4`) e as 5 colunas da direita (`X = 15..19`) possuem colisão sólida (`0x0F`).
  - O carro só pode trafegar dentro das 10 colunas centrais de asfalto (`X = 5..14`), impedindo que o jogador saia da estrada para desviar dos obstáculos.

---

## 3. Sistema de Obstáculos e Colisão (`Game Over`)
- Cada fase contém **27 atores** representando os 4 tipos de obstáculos:
  1. **Carro Azul** (`carro_azul.png`)
  2. **Carro Verde** (`carro_verde.png`)
  3. **Cone** (`cone.png`)
  4. **Pedra** (`pedra.png`)
- **Detecção de Batida (`hit1Script`):**
  - Todos os obstáculos estão configurados no `collisionGroup: "1"`.
  - No script da cena (`hit1Script`), assim que o jogador colide com qualquer ator do grupo `1`:
    1. Toca imediatamente um efeito sonoro de colisão (`type: "crash"`).
    2. Executa `EVENT_SWITCH_SCENE` levando o jogador para a cena **Game Over (`game_over` / `LOSE.png`)**.

---

## 4. Linha Branca de Chegada e Progressão de Fases
- No final (topo) de cada estrada (`Y = 2..3`, `X = 5..14`), há uma **faixa branca pintada no asfalto** acompanhada de um **Trigger (`Linha de Chegada`)**:
  - **Fase 1 (Grama):** Cruzar a linha branca toca um efeito sonoro de avanço (`tone`) e carrega a **Fase 2 (Deserto)**.
  - **Fase 2 (Deserto):** Cruzar a linha branca carrega a **Fase 3 (Mar)**.
  - **Fase 3 (Mar):** Cruzar a linha branca carrega a **Fase 4 (Neve)**.
  - **Fase 4 (Neve):** Cruzar a linha branca final carrega a tela de **Vitória (`vitoria` / `WIN.png`)**, consagrando o jogador campeão da **Copa dos Quatro Climas**.
