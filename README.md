# Agentic Chess using Min-Max Algorithm and Pygame

> An intelligent chess game featuring AI opponent using the Min-Max algorithm, built with Python and Pygame.

[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-3776ab?style=flat-square&logo=python)](https://www.python.org/)
[![Pygame](https://img.shields.io/badge/Pygame-Powered-red?style=flat-square)](https://www.pygame.org/)
[![License MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)

## 📋 Overview

**Agentic Chess** is a fully-featured chess game with an intelligent AI opponent powered by the **Min-Max algorithm**. Play against a smart AI that evaluates chess positions and makes strategic decisions. Built with **Pygame** for smooth graphics and interactive gameplay, this project demonstrates classical game theory algorithms and game development techniques.

Ideal for learning AI decision-making, game development, and implementing minimax search algorithms.

## ✨ Key Features

- ♟️ **Full Chess Rules** — Complete implementation of standard chess rules
- 🤖 **AI Opponent** — Min-Max algorithm with alpha-beta pruning for intelligent moves
- 🎮 **Interactive GUI** — Smooth, responsive Pygame interface
- 📊 **Move Analysis** — See AI evaluation and thinking depth
- ♻️ **Game History** — Track all moves and undo functionality
- 🏁 **Game States** — Checkmate, stalemate, and draw detection
- ⏱️ **Difficulty Levels** — Adjustable AI search depth
- 💾 **Save/Load Games** — Persist game state

## 🏗️ Architecture

### Tech Stack

| Component | Technology |
|-----------|------------|
| **Game Engine** | Pygame |
| **Language** | Python 3.8+ |
| **AI Algorithm** | Min-Max with Alpha-Beta Pruning |
| **Logic** | Chess rule engine |

### Algorithm Overview

**Min-Max Algorithm**: A decision-making algorithm that recursively evaluates all possible moves and counter-moves to a certain depth, choosing the move that maximizes the AI's advantage while assuming the opponent plays optimally.

**Alpha-Beta Pruning**: Optimization technique that eliminates branches that won't affect the final decision, significantly speeding up the search.

### Project Structure

```
chess-ai/
├── src/
│   ├── main.py              # Application entry point
│   ├── game/
│   │   ├── board.py         # Chess board logic
│   │   ├── pieces.py        # Piece classes and movements
│   │   ├── rules.py         # Chess rule engine
│   │   └── state.py         # Game state management
│   ├── ai/
│   │   ├── minimax.py       # Min-Max algorithm
│   │   ├── evaluator.py     # Position evaluation
│   │   └── solver.py        # AI decision making
│   ├── ui/
│   │   ├── board_display.py # Board rendering
│   │   ├── ui_components.py # UI elements
│   │   └── renderer.py      # Graphics
│   └── utils/
│       ├── constants.py     # Game constants
│       └── helpers.py       # Utility functions
├── assets/
│   ├── pieces/              # Piece sprites
│   └── sounds/              # Game sounds
├── requirements.txt         # Dependencies
└── README.md               # This file
```

## 🚀 Getting Started

### Prerequisites

- **Python 3.8** or higher
- **pip** package manager
- **Git**

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Maliksaad69/Agentic-Chess-using-Min-Max-algorithm-using-Pygame.git
   cd Agentic-Chess-using-Min-Max-algorithm-using-Pygame
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv venv
   
   # Windows:
   venv\Scripts\activate
   # macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

### Running the Game

```bash
python src/main.py
```

The chess game will open in a Pygame window. Play as White (bottom), AI plays as Black (top).

## 🎮 How to Play

### Basic Controls

| Action | Control |
|--------|---------|
| **Select Piece** | Click on a piece |
| **Move Piece** | Click on destination square |
| **Undo Move** | Press `U` or click Undo |
| **New Game** | Press `N` or click New Game |
| **Quit** | Close window or press `Q` |

### Game Rules

- Move pieces according to standard chess rules
- Each piece has specific movement patterns:
  - **Pawn**: Forward 1-2 squares (first move), capture diagonally
  - **Knight**: L-shaped jumps
  - **Bishop**: Diagonals
  - **Rook**: Horizontal/Vertical
  - **Queen**: Any direction
  - **King**: Adjacent squares

- Win by checkmating the opponent
- Game ends in stalemate if no legal moves available
- Threefold repetition or 50-move rule results in a draw

## 🤖 AI Configuration

### Difficulty Levels

Adjust AI strength by modifying search depth in `constants.py`:

```python
AI_SEARCH_DEPTH = 4  # Change this value
# 2-3: Beginner (fast, weaker)
# 4-5: Intermediate (balanced)
# 6+: Advanced (slow, stronger)
```

### Evaluation Function

The AI evaluates board positions using:
- Piece material value (Pawn=1, Knight=3, Bishop=3, Rook=5, Queen=9)
- Piece positioning bonuses
- King safety
- Pawn structure

### Performance Optimization

The Min-Max algorithm with alpha-beta pruning makes the search feasible:
- Without pruning: ~35^6 positions at depth 6
- With alpha-beta: ~1% of positions evaluated

## 📊 Algorithm Deep Dive

### Min-Max Pseudocode

```python
def minimax(board, depth, is_maximizing, alpha, beta):
    if depth == 0 or game_over(board):
        return evaluate(board)
    
    if is_maximizing:
        max_score = -infinity
        for move in legal_moves(board):
            apply_move(board, move)
            score = minimax(board, depth-1, False, alpha, beta)
            undo_move(board)
            max_score = max(max_score, score)
            alpha = max(alpha, score)
            if beta <= alpha:
                break  # Alpha-beta pruning
        return max_score
    else:
        min_score = +infinity
        for move in legal_moves(board):
            apply_move(board, move)
            score = minimax(board, depth-1, True, alpha, beta)
            undo_move(board)
            min_score = min(min_score, score)
            beta = min(beta, score)
            if beta <= alpha:
                break  # Alpha-beta pruning
        return min_score
```

## 🧪 Testing

Run tests with:

```bash
# Run all tests
python -m pytest tests/

# Test chess rules
python -m pytest tests/test_rules.py

# Test AI algorithm
python -m pytest tests/test_minimax.py

# With coverage
python -m pytest --cov=src tests/
```

## 🗺️ Roadmap

- [ ] Opening book integration (known good first moves)
- [ ] Transposition table (memoization)
- [ ] Iterative deepening search
- [ ] Endgame tablebase support
- [ ] Network play (online multiplayer)
- [ ] Game replay and analysis
- [ ] UCI protocol support (play with other engines)
- [ ] Machine learning evaluation function

## 🤝 Contributing

Contributions are welcome!

1. **Fork** the repository
2. **Create feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit changes**
   ```bash
   git commit -m "feat: Add amazing feature"
   ```
4. **Push to branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open Pull Request**

### Areas for Contribution

- Improve AI evaluation function
- Add more move optimization strategies
- Enhanced UI/UX
- Performance optimizations
- Additional game features

## 📄 License

Licensed under the **MIT License** — see [LICENSE](LICENSE) file.

## 💬 Support & Contact

- **GitHub Issues**: [Report issues](https://github.com/Maliksaad69/Agentic-Chess-using-Min-Max-algorithm-using-Pygame/issues)
- **Email**: malik@example.com
- **Twitter**: [@Maliksaad69](https://twitter.com/Maliksaad69)

## 📚 Learning Resources

- [Chess Rules](https://www.chess.com/terms/chess-rules)
- [Min-Max Algorithm](https://en.wikipedia.org/wiki/Minimax)
- [Alpha-Beta Pruning](https://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning)
- [Pygame Documentation](https://www.pygame.org/docs/)
- [Game Theory Basics](https://en.wikipedia.org/wiki/Game_theory)

## 🙏 Acknowledgments

- Chess community for rules and conventions
- Pygame team for the excellent library
- Game AI research community
- All contributors and supporters!

---

**Built with ❤️ by [Malik Saad](https://github.com/Maliksaad69) | [⭐ Star on GitHub](https://github.com/Maliksaad69/Agentic-Chess-using-Min-Max-algorithm-using-Pygame)**
