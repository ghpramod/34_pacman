# Pac-Man Repair Lab — Lab 4: VibeCoding

This project is a single-file Pac-Man-lite clone using **Pygame**. It introduces students to grid movement, pellet collection, and ghost AI targeting rules using a small, readable object-oriented codebase.

---

## What's Provided

A working Pac-Man-lite game with:

- Grid-based movement with wall collision and pellet collection
- Four ghosts with distinct targeting behavior (Blinky chases directly, Pinky ambushes ahead of the player, Inky uses Blinky's position, Clyde flees when close) on a shared scatter/chase timer
- Frightened mode when a power pellet is eaten, with ghosts reversing direction once and becoming eatable
- Lives, scoring, and win/lose conditions

---

## Getting Started

### Setup

1. Make sure you have Python 3.10+ installed.
2. Install dependencies:

```bash
pip install pygame
```

3. Run the game:

```bash
python game.py
```

**Controls:** Arrow keys to move, `R` to reset.

---

## Tasks Completed (VibeCoding Iterations)

### Task 1: Fix the power pellet bug [COMPLETED]

- **Issue:** Eating a power pellet previously gave only 10 points and never triggered frightened mode.
- **Root Cause:** In `MAZE`, power pellets are represented with lowercase `'o'`, but `eat()` checked `MAZE[cell[0]][cell[1]] == "O"` with uppercase `'O'`.
- **Fix:** Updated comparison to `if MAZE[cell[0]][cell[1]] in ("o", "O"):`. Now grants +40 bonus points, sets `fright_left = FRIGHT_SECONDS`, and reverses non-eaten ghosts.

### Task 2: Implement `ghost_color(name, mode)` [COMPLETED]

- **Implementation:** When `mode == "frightened"`, assigns each ghost a distinct, recognizable frightened tint:
  - **Blinky:** Royal Indigo `(65, 85, 245)`
  - **Pinky:** Lilac / Orchid Violet `(185, 95, 225)`
  - **Inky:** Cyan / Seafoam Turquoise `(45, 200, 215)`
  - **Clyde:** Periwinkle / Steel Blue `(100, 150, 235)`
- Returns `None` for `"normal"` and `"eaten"` to retain default colors and returning-eyes sprites.

### Task 3: Implement `on_pellet_eaten(score, pellets_left)` [COMPLETED]

- **Implementation:** Spawns a collectible bonus cherry at `(7, 10)` outside the ghost house when remaining pellets hit milestones (115, 80, 40 remaining).
- Collecting the cherry awards **+100 bonus points** and displays a HUD pickup notification.
- Flashes HUD when `pellets_left == 1` indicating the final pellet.

### Task 4: Implement `bonus_life_threshold()` [COMPLETED]

- **Implementation:** Returns `500`. Calibrated for the 130-pellet mini-maze so an extra life is awarded automatically every 500 points.
- Automatically increments `self.lives += 1` and flashes `[BONUS LIFE AWARDED!]` on the HUD.

---

## Deliverables & Folder Structure

```
34_pacman/
├── game.py                        # Updated functional game
├── README.md                      # Documentation & report
├── Lab-4/
│   ├── before_fix_gameplay.mp4    # 10s video showing broken power pellet
│   ├── after_fix_gameplay.mp4     # 10s video showing fixed game & all features
│   ├── game.py                    # Complete updated game script
│   ├── chat_history.pdf           # Exported LLM conversation transcript
│   ├── chat_history.docx          # Word doc format export
│   └── README.md                  # Lab-4 documentation
```

---

## Submission Checklist

- [x] A 10-second video of gameplay **before** your changes, showing the bug/broken behavior (`Lab-4/before_fix_gameplay.mp4`)
- [x] A 10-second video of gameplay **after** your changes, showing the bug fixed and the new features working (`Lab-4/after_fix_gameplay.mp4`)
- [x] The Chat/LLM used complete chat history exported as PDF/DOC (`Lab-4/chat_history.pdf`, `Lab-4/chat_history.docx`)
