# ♟️ Chess — Human vs Bot

A lightweight, modern, and fully interactive web-based chess application featuring a custom JavaScript chess engine running in a background Web Worker. Play against a calculating AI directly in your browser with no backend required.

🌐 **Live Demo:** [chess.namansoni.in](https://chess.namansoni.in)

---

## ✨ Features

- 🧠 **Custom In-Browser Chess Engine**: Built using Negamax with Alpha-Beta pruning, running off the main UI thread via Web Workers.
- 🎯 **Multiple Difficulty Levels**: Choose from 4 difficulty levels with configurable thinking time and search depth.
- 🎨 **Modern Responsive UI**: Clean dark-mode interface designed for desktop and mobile screens.
- 🔊 **Web Audio Sound Effects**: Optional audio cues for moves, captures, and checks created dynamically with the Web Audio API.
- 📜 **Full Move History**: Move notation log using standard algebraic notation (SAN) with automatic auto-scrolling.
- 🔄 **Game Controls**: Flip board view, undo turns, resign, or adjust play settings on the fly.
- ♟️ **Pawn Promotion Dialog**: Modal interface for choosing pawn promotion pieces (Queen, Rook, Bishop, Knight).
- ⚖️ **Automatic Draw Detection**: Detects threefold repetition, 50-move rule, stalemate, and insufficient material.

---

## ⚙️ Engine Architecture & AI Details

The AI engine runs entirely inside a dedicated **Web Worker**, ensuring the UI remains smooth (60 FPS) even during heavy search calculations.

### Search & Optimization Techniques
1. **Negamax Engine with Alpha-Beta Pruning**: Reduces the search space efficiently while finding optimal moves.
2. **Iterative Deepening**: Progressively searches deeper depths within the allocated time budget, guaranteeing a valid move if search is interrupted.
3. **Transposition Table**: Caches evaluated board positions to avoid redundant evaluations.
4. **Quiescence Search**: Evaluates tactical sequences (captures & promotions) beyond the nominal search depth to prevent the "horizon effect".
5. **Advanced Move Ordering**:
   - Transposition Table best moves.
   - **MVV-LVA** (Most Valuable Victim - Least Valuable Attacker) for captures.
   - **Killer Move Heuristic** for non-captures that caused beta cutoffs.
   - **History Heuristic** scoring for effective quiet moves.
6. **Positional Evaluation Function**:
   - Material values ($P=100, N=320, B=335, R=500, Q=900, K=20000$).
   - Phase-based evaluation transition (Opening/Middlegame vs. Endgame).
   - Positional bonuses: Center control, pawn structure (doubled/isolated/passed pawns), bishop pair bonus, rook open file placement, and king safety/shelter.

---

## 📊 Difficulty Levels

| Difficulty | Search Time Limit | Max Search Depth | Best For |
| :--- | :--- | :--- | :--- |
| **Quick** | 0.5 seconds | Depth 3 | Fast casual play / beginners |
| **Balanced** | 1.5 seconds | Depth 5 | Balanced challenge |
| **Strong** | 4.0 seconds | Depth 7 | Tactical players looking for a challenge |
| **Deep** | 8.0 seconds | Depth 9 | Deep positional search |

---

## 🛠️ Tech Stack

- **Frontend**: HTML5, CSS3 (CSS Grid, Flexbox, CSS Variables), Vanilla JavaScript (ES6+).
- **Engine Logic**: JavaScript Web Workers, Negamax search tree.
- **Rules & Move Validation**: [chess.js](https://github.com/jhlywa/chess.js) (v0.10.3).
- **Audio**: Native Browser Web Audio API.

---

## 🚀 Local Development & Setup

No node packages or build tools are required to run the project.

### Running Locally

Since Web Workers require same-origin security policies, serve the project using any static file web server:

```bash
# Clone the repository
git clone https://github.com/namansoni/chess.git
cd chess

# Option 1: Using Python 3
python3 -m http.server 8000

# Option 2: Using Node http-server / npx
npx serve .
```

Open your browser at `http://localhost:8000` (or the URL provided by your server).

---

## 📝 License

Distributed under the MIT License. Feel free to use, modify, and distribute this software.
