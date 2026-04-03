# Requirements Document

## 1. Application Overview
- **App Name:** Swift Strike
- **Description:** A fast-paced side-scrolling action game where the player fights through waves of enemies using quick attacks and dodges, aiming to survive as long as possible and achieve a high score.

---

## 2. Page Structure & Feature Description

### Overall Structure
```
Swift Strike
├── Main Menu Page
├── Gameplay Page
└── Game Over Page
```

### 2.1 Main Menu Page
- Displays the game title: Swift Strike
- Buttons:
  - Start Game: enters the Gameplay Page
  - Best Score: displays the locally stored highest score
- Simple animated background to set the action tone

### 2.2 Gameplay Page
**Player Character**
- Spawns on the left side of the screen
- Movement: left / right / jump (keyboard arrow keys or WASD)
- Attack: melee strike (Z key or J key), short-range, fast cooldown (~0.3s)
- Dodge/Dash: quick horizontal dash (X key or K key), brief invincibility frames (~0.2s), cooldown ~1.5s
- Health: 3 hit points (HP); displayed as a health bar at the top-left

**Enemies**
- Spawn from the right side of the screen at regular intervals
- Basic enemy type: moves toward the player and deals contact damage
- Spawn rate increases gradually over time to raise difficulty
- Each enemy defeated awards 10 points

**Score & Timer**
- Current score displayed at the top-right
- Elapsed survival time displayed at the top-center
- Score increases by defeating enemies; no time-based bonus

**Game End Condition**
- Game ends when the player's HP reaches 0
- Transitions automatically to the Game Over Page

### 2.3 Game Over Page
- Displays: final score and survival time
- If the final score exceeds the stored best score, update and highlight it as a new record
- Buttons:
  - Retry: restarts the game immediately
  - Main Menu: returns to the Main Menu Page

---

## 3. Business Rules & Logic

| Rule | Description |
|---|---|
| Enemy spawn interval | Starts at 2s; decreases by 0.1s every 15s, minimum interval 0.5s |
| Player invincibility after hit | 1.5s of invincibility frames after taking damage to prevent instant multi-hit |
| Dash cooldown | 1.5s; dash cannot be chained consecutively |
| Attack cooldown | ~0.3s; rapid tapping allowed within cooldown limit |
| Best score persistence | Stored in browser local storage; persists across sessions |
| Collision detection | Enemy contact with player body = 1 HP damage; attack hitbox must connect with enemy body to deal damage |

---

## 4. Edge Cases & Boundary Conditions

| Scenario | Handling |
|---|---|
| Player reaches screen left boundary | Player stops moving; cannot go off-screen |
| Multiple enemies hit simultaneously | Each collision counted separately; invincibility frames prevent stacking damage |
| Player attacks with no enemies present | Animation plays normally; no effect |
| Dash used at screen edge | Dash distance clamped to screen boundary |
| Score overflows display area | Score display truncated or scaled to fit UI |

---

## 5. Acceptance Criteria

- Player character responds to movement, attack, and dash inputs with no noticeable delay
- Enemies spawn from the right and move toward the player; spawn rate increases over time
- HP bar decreases correctly upon taking damage; invincibility frames prevent multi-hit within the window
- Score increments correctly upon each enemy defeat
- Game Over Page displays correct final score and survival time
- New best score is saved and displayed correctly on both the Game Over Page and Main Menu
- Retry and Main Menu buttons function correctly
- Game runs smoothly without frame drops during normal enemy density

---

## 6. Out of Scope for This Version

- Multiple levels or stage-based progression
- Boss enemies or special enemy types
- Player skill upgrades or power-up items
- Background music or sound effects
- Multiplayer or online leaderboard
- Mobile touch controls
- Cutscenes or narrative content