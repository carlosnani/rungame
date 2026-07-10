# 🏃‍♀️ Corre Amanda!

Um clone do jogo do dinossauro do Chrome, completamente reimplementado em HTML5 Canvas com sprites personalizados, power-ups e sistema de parallax.

**[🎮 JOGUE AGORA](https://carlosnani.github.io/rungame/)**

## 🎮 Como Jogar

| Controle | Ação |
|----------|------|
| `Espaço` / `↑` | Pular |
| `↓` | Agachar |
| Toque na tela (mobile) | Pular |
| Toque na parte inferior (mobile) | Agachar |

## ✨ Funcionalidades

### Gameplay
- **Sistema de velocidade progressiva** — o jogo fica mais rápido conforme a pontuação aumenta
- **Colisão justa** — hitbox do jogador é levemente menor que o visual para fairness
- **Recorde persistente** — salvo automaticamente no `localStorage`

### Sprites Animados
- **Jogador** — spritesheet 3×2 com animações de corrida, pulo e agachamento
- **Inimigos** — spritesheet `inimigo_.png` 3×2 com 6 frames de animação
- **Fallback em canvas** — se as imagens não carregarem, o jogo continua com desenhos geométricos

### Power-ups ⚡
| Power-up | Efeito |
|----------|--------|
| ⭐ **Invencibilidade** | Esmaça inimigos ao tocar |
| ⚡ **Score Boost** | Pontuação em dobro por 5 segundos |
| 🛡 **Escudo** | Absorve um golpe |

### Coletáveis
- **Estrelas** — +50 pontos cada
- **Power-ups** — aparecem aleatoriamente a cada 400–700 frames

### Visual
- **Tela de título animada** — logo com efeito de entrada, prompt pulsante, e exibição do recorde
- **Nuvens com parallax** — 3 camadas de profundidade com velocidades e opacidades diferentes
- **Efeitos de colisão** — tela treme ao perder (shake animation)
- **HUD aprimorado** — contador de estrelas, barra de timer de power-ups

### Responsividade
- Layout adaptável para telas de 480px até 1440px+
- `prefers-reduced-motion` respeitado (desativa animações CSS)

## 🚀 Como Executar

```bash
# Clone o repositório
git clone https://github.com/carlosnani/rungame.git
cd rungame

# Abra o index.html no navegador
# No Windows:
start index.html

# No macOS:
open index.html

# No Linux:
xdg-open index.html
```

> **Nota:** O jogo funciona sem servidor — basta abrir o arquivo `index.html` diretamente no navegador.

## 📁 Estrutura do Projeto

```
rungame/
├── index.html              # Jogo principal (HTML + CSS + JS em um arquivo)
├── README.md
├── img/
│   ├── sprite-animation.png   # Spritesheet do jogador (3×2 frames)
│   ├── inimigo_.png           # Spritesheet dos inimigos (3×2, 2048×2048)
│   ├── title.png              # Logo da tela de título
│   └── *.gif                  # Versões GIF das animações
└── .agents/                   # Skills de assistente AI
```

## 🛠 Tecnologias

- **HTML5 Canvas** — renderização 2D de alta performance
- **JavaScript vanilla** — sem frameworks ou dependências externas
- **CSS3** — animações e responsividade
- **Spritesheet rendering** — recorte de frames via `drawImage` e `background-position`

## 🎯 Arquitetura do Jogo

### Game Loop
O jogo utiliza `requestAnimationFrame` para um loop de 60fps com three-phase state machine:

```
WAITING → (pressiona espaço) → PLAYING → (colisão) → GAME_OVER → (espaço) → PLAYING
```

### Sistema de Colisão
- **AABB** para retângulos (jogador × inimigos)
- **AABB vs Círculo** para coletáveis (jogador × estrelas/power-ups)

### Rendering Pipeline
1. `drawSky()` — fundo branco
2. `drawClouds()` — nuvens parallax
3. `drawGround()` — chão e textura
4. `drawEnemy()` — inimigos com spritesheet
5. `drawCollectibles()` — estrelas e power-ups
6. `drawFallbackPlayer()` — fallback do jogador (se sprite falhar)
7. `drawScore()` / `drawEnhancedHUD()` / `drawUI()` — interface

## 📄 Licença

Este é um projeto educacional. Os sprites e assets são de uso pessoal.
