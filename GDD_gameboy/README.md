# Visão Geral do Jogo

**Título Oficial:** *Horizon Rush GBC: A Copa dos Quatro Climas* *(Título Provisório Original: Super Retro Drive)*  
**Gênero:** Corrida Arcade Top-Down / Desvio de Obstáculos (*Action Racing*)  
**Plataforma:** Game Boy Color (desenvolvido no **GB Studio 4.3.2**)  
**Resolução Nativa:** `160x144` pixels (Mapas de fase com `160x1600` pixels em rolagem vertical)

---

## Sinopse e História
Bem-vindo à **Copa dos Quatro Climas**, o rally continental mais extremo do mundo! Você pilota o lendário **Relâmpago Rubro** (*Red Viper*), um protótipo esportivo vermelho cujo sistema de injeção eletrônica travou o acelerador no máximo logo na largada.

Sem freios e em velocidade alucinante, você precisa cruzar quatro regiões climáticas implacáveis — **Planícies Esmeralda (Grama)**, **Cânion Escaldante (Deserto)**, **Ponte Atlântica (Mar)** e **Pico Boreal (Neve)** — desviando de corredores rivais (**Carros Azuis e Verdes**), **Cones de sinalização** e **Pedras na pista** até cruzar a linha branca final de cada etapa.

Veja a história completa em: [[Historia]] (`HISTORIA/Historia.md`)

---

## Core Loop (Fluxo Principal do Jogo)
1. **Menu Inicial (`Menu`):** O jogador inicia na tela título ao som de abertura e pressiona **START** ou **A** para largar.
2. **Avanço Automático:** O carro vermelho acelera automaticamente rumo ao topo da estrada (`Y = 195` até `Y = 3`).
3. **Desvio Lateral:** O jogador utiliza **D-Pad Esquerda / Direita** para mudar de faixa na pista e escapar de **27 obstáculos** por fase (Carros Azuis, Carros Verdes, Cones e Pedras).
4. **Colisão (`Game Over`):** Encostar em qualquer obstáculo leva imediatamente à tela de derrota (`LOSE`), permitindo tentar novamente do início pressionando **START**, **A** ou **B**.
5. **Linha Branca de Chegada (Progressão de Fases):** Ao alcançar a faixa branca no final da pista (`Y = 2..3`), o jogador avança para o próximo bioma:
   - **Fase 1:** Estrada / Grama (`estrada_grama`) ->
   - **Fase 2:** Estrada / Deserto (`estrada_deserto`) ->
   - **Fase 3:** Estrada / Mar (`estrada_mar`) ->
   - **Fase 4:** Estrada / Neve (`estrada_neve`) ->
   - **Tela Final:** Vitória (`WIN`)!

---

## Trilha Sonora e Efeitos Sonoros (`hUGEDriver` / `.uge`)
O jogo conta com trilha sonora em 4 canais reais do Game Boy (`Duty 1`, `Duty 2`, `Wave` e `Noise`):
- **Fases 1 a 4 (Corrida):** `topgear1.uge` — Conversão customizada do clássico tema *Top Gear - Track 1 (Mad Racer)* de Barry Leitch a partir de `topgear1.mid` para o formato `.uge` v6 (melodia em onda quadrada 50%, arpejos em pulso 12.5%/25% com eco estéreo, baixo *Sawtooth* no canal Wave e bateria *Kick/Snare/Hi-Hat* no canal Noise).
- **Menu Inicial:** `Rulz_Intro.uge`
- **Tela de Vitória (`WIN`):** `Rulz_LightMood.uge` + efeito sonoro de confirmação.
- **Tela de Derrota (`LOSE`):** `Rulz_Pause_Underground.uge` + efeito sonoro de batida (`crash`).

---

## Índice da Documentação (GDD)
- **História e Universo:** [[Historia]] (`HISTORIA/Historia.md`)
- **Personagem (Jogador):** [[Personagem]] (`PERSONAGEM/Personagem.md`)
- **Obstáculos e Rivais:** [[Inimigos]] (`INIMIGOS/Inimigos.md`)
- **Mapas, Fases e Telas:** [[Cenario 1 - Estrada]] (`MAPA/Cenario 1 - Estrada.md`)
- **Mecânicas e Sistema GB Studio:** [[Mecanicas]] (`MECANICAS/Mecanicas.md`)
- **Controles:** [[Controles]] (`CONTROLES/Controles.md`)
- **Limitações Técnicas e Adaptações GBC:** [[Limitacoes]] (`Limitacoes.md`)
