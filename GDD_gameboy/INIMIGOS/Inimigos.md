# Obstáculos e Corredores Rivais

Durante as 4 etapas de **Horizon Rush GBC**, o jogador precisa desviar de **4 tipos de obstáculos** distribuídos ao longo da estrada. Em cada fase há **27 obstáculos** posicionados estrategicamente nas faixas da pista (totalizando **108 obstáculos** ao longo das 4 fases).

Todos os obstáculos pertencem ao **Grupo de Colisão 1 (`collisionGroup: "1"`)** e causam **Game Over instantâneo** ao tocar no carro do jogador.

---

## 1. Carro Azul — Equipe Safira (`carro_azul`)
Corredores rivais da *Equipe Safira* que ocupam as faixas da rodovia tentando bloquear a ultrapassagem do jogador.

- **Sprite:** `Sprites/Png/CarroAzul.png`
  ![[CarroAzul.png]]
- **Dimensões:** `16x16` pixels
- **Paleta GBC (Slot 1 — `pal_carro_azul.gbsres`):**
  - Claro (Faróis/Detalhes): `#F8F038` (Amarelo)
  - Médio (Lataria): `#4070C0` (Azul Royal)
  - Escuro (Pneus/Chassi): `#181818` (Preto)
- **Hitbox:** `boundsX: 2`, `boundsY: -2`, `boundsWidth: 12`, `boundsHeight: 11`

---

## 2. Carro Verde — Equipe Esmeralda (`carro_verde`)
Corredores rivais da *Equipe Esmeralda*, posicionados em trechos de zigue-zague e duplas de bloqueio parcial na pista.

- **Sprite:** `Sprites/Png/CarroVerde.png`
  ![[CarroVerde.png]]
- **Dimensões:** `16x16` pixels
- **Paleta GBC (Slot 2 — `pal_carro_verde.gbsres`):**
  - Claro (Faróis/Detalhes): `#F8F038` (Amarelo)
  - Médio (Lataria): `#68C030` (Verde Vibrante)
  - Escuro (Pneus/Chassi): `#181818` (Preto)
- **Hitbox:** `boundsX: 2`, `boundsY: -2`, `boundsWidth: 12`, `boundsHeight: 11`

---

## 3. Cone de Sinalização (`cone`)
Cones laranjas e brancos deixados por equipes de manutenção rodoviária ao longo do asfalto.

- **Sprite:** `Sprites/Png/cone.png`
  ![[cone.png]]
- **Dimensões:** `16x16` pixels
- **Paleta GBC (Slot 3 — `pal_cone.gbsres`):**
  - Claro (Faixa Refletiva): `#F8F8F8` (Branco)
  - Médio (Corpo do Cone): `#E86820` (Laranja)
  - Escuro (Base/Sombra): `#202038` (Azul-escuro/Grafite)
- **Hitbox:** `boundsX: 3`, `boundsY: -2`, `boundsWidth: 10`, `boundsHeight: 10`

---

## 4. Pedra na Pista (`pedra`)
Rochas pesadas que rolaram para o meio da estrada a partir das encostas, dunas e montanhas.

- **Sprite:** `Sprites/Png/Pedra.png`
  ![[Pedra.png]]
- **Dimensões:** `16x16` pixels
- **Paleta GBC (Slot 4 — `pal_pedra.gbsres`):**
  - Claro (Reflexo Superior): `#A0A0A0` (Cinza Claro)
  - Médio (Rocha): `#606060` (Cinza Médio)
  - Escuro (Sombra/Base): `#080808` (Preto)
- **Hitbox:** `boundsX: 3`, `boundsY: -3`, `boundsWidth: 10`, `boundsHeight: 8`

---

## Regras de Design e Distribuição nas Fases
- **Limite por Cena do GB Studio:** Cada uma das 4 fases possui exatamente **27 atores de obstáculos** distribuídos entre `Y = 18` e `Y = 180` nas colunas da pista (`X = 5` a `X = 13`).
- **Limite de Scanline Respeitado:** Nunca há mais de **2 obstáculos na mesma linha horizontal (eixo Y)**. Assim, somando o carro do jogador (2 *hardware sprites*) + até 2 obstáculos na mesma altura (4 *hardware sprites*), a cena usa no máximo **6 sprites por linha**, ficando bem abaixo do limite de 10 sprites por *scanline* do Game Boy Color (zero *flickering*).
- **Passagem Sempre Garantida (*Regra de Ouro*):** A largura útil da pista é de 10 tiles (`X = 5..14`). Mesmo quando há 2 obstáculos na mesma altura, sempre restam faixas livres com largura suficiente para a passagem do **Relâmpago Rubro**.
