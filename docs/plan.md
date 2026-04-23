# Snake Game Implementation

## Goal Description

Create a fully functional snake game (贪吃蛇) as a web-based game using HTML, CSS, and JavaScript. The game includes core snake movement mechanics, food spawning, collision detection, score tracking with localStorage persistence, pause/restart functionality, and a polished user interface.

## Acceptance Criteria

Following TDD philosophy, each criterion includes positive and negative tests for deterministic verification.

- AC-1: Game Core Functionality
  - Positive Tests (expected to PASS):
    - Snake moves continuously in the current direction at consistent speed
    - Snake responds to arrow key controls (↑↓←→) and changes direction
    - Snake grows by one segment when eating food
    - Food spawns in random valid positions not occupied by snake
  - Negative Tests (expected to FAIL):
    - Snake cannot reverse direction into itself (e.g., going right cannot immediately go left)
    - Snake cannot pass through walls - collision triggers game over
    - Game ends when snake collides with itself
  
- AC-2: Score System
  - Positive Tests (expected to PASS):
    - Score increases by 10 points when snake eats food
    - Current score displays in real-time in the UI
    - High score is saved to localStorage and persists across page refreshes
  - Negative Tests (expected to FAIL):
    - Score does not increase when snake is not eating food
    - High score does not reset on page refresh (persists correctly)
  
- AC-3: Game State Management
  - Positive Tests (expected to PASS):
    - Game can be paused by pressing Space key
    - Game can be restarted after game over via button click
    - Game starts automatically when page loads
  - Negative Tests (expected to FAIL):
    - Arrow keys do not change snake direction when game is paused
    - Game loop stops completely when game over occurs
  
- AC-4: User Interface
  - Positive Tests (expected to PASS):
    - Canvas renders game at smooth 60fps (100ms interval)
    - Score updates immediately when food is eaten
    - Game over screen displays final score and restart button
  - Negative Tests (expected to FAIL):
    - UI elements do not flicker during game play
    - Score never displays negative values

## Path Boundaries

Path boundaries define the acceptable range of implementation quality and choices.

### Upper Bound (Maximum Acceptable Scope)

The implementation includes a polished snake game with all core features, score persistence via localStorage, pause/resume functionality via Space key, difficulty levels (easy/medium/hard with varying speed), responsive canvas that adapts to viewport, keyboard-only controls with visual instructions, and a clean modern UI with smooth animations.

### Lower Bound (Minimum Acceptable Scope)

The implementation includes core snake movement with arrow key controls, food spawning and eating mechanics, wall and self-collision detection, basic score tracking displayed in UI, game over detection with restart capability, and a simple canvas-based rendering with straightforward visual design.

### Allowed Choices

- Can use: HTML5 Canvas for rendering, vanilla JavaScript (no frameworks), CSS for styling, localStorage API for score persistence
- Cannot use: External game libraries or frameworks, server-side code, complex build tools (single HTML file preferred)

> **Note on Deterministic Designs**: The draft specifies a simple snake game with no specific technical requirements. The path boundaries above reflect reasonable flexibility while ensuring core functionality.

## Feasibility Hints and Suggestions

> **Note**: This section is for reference and understanding only. These are conceptual suggestions, not prescriptive requirements.

### Conceptual Approach

```
Game Loop (100ms interval):
1. Calculate new head position based on current direction
2. Check wall collision → Game Over if hit
3. Check self-collision → Game Over if hit
4. Check food collision → Score +10, Grow snake, Spawn new food
5. Move snake (unshift new head, pop tail unless eating)
6. Render all elements to canvas

Input Handling:
- Arrow keys: Change direction (validate no reverse)
- Space key: Toggle pause state
- Enter/Click: Restart after game over
```

### Relevant References

- `/app/workspaces/2fb0c19a-387e-4eb9-9cc2-fdabb3dbf4a2/snake.html` - Existing snake game implementation for reference
- Canvas 2D API - MDN documentation for rendering
- localStorage API - For high score persistence

## Dependencies and Sequence

### Milestones

1. **Milestone 1**: Core Game Mechanics
   - Phase A: Set up HTML structure with canvas element
   - Phase B: Implement snake movement and rendering
   - Phase C: Add food spawning and eating logic

2. **Milestone 2**: Game Features
   - Phase A: Implement collision detection (walls and self)
   - Phase B: Add score system with UI display
   - Phase C: Implement game over and restart functionality

3. **Milestone 3**: Polish
   - Phase A: Add pause/resume with Space key
   - Phase B: Implement localStorage for high score persistence
   - Phase C: Final UI polish and testing

## Task Breakdown

Each task must include exactly one routing tag:

| Task ID | Description | Target AC | Tag (`coding`/`analyze`) | Depends On |
|---------|-------------|-----------|----------------------------|------------|
| task1 | Set up HTML structure with canvas and basic CSS styling | AC-4 | coding | - |
| task2 | Implement snake movement and rendering logic | AC-1 | coding | task1 |
| task3 | Add food spawning and collision detection | AC-1 | coding | task2 |
| task4 | Implement score system with localStorage persistence | AC-2 | coding | task3 |
| task5 | Add game state management (pause, restart, game over) | AC-3 | coding | task4 |
| task6 | Final testing and README documentation | AC-1, AC-2, AC-3, AC-4 | coding | task5 |

## Claude-Codex Deliberation

### Agreements

- Both Claude and Codex agree that the snake game is a straightforward web development project
- Both agree that single HTML file structure is appropriate for this project
- Both agree that localStorage should be used for score persistence

### Resolved Disagreements

- **Project scope**: Claude initially considered a more complex multi-file structure; Codex recommended keeping it simple given the draft's simplicity. Resolution: Single HTML file with embedded CSS/JS, matching the existing project style.

### Convergence Status

- Final Status: `partially_converged`

**Note**: In `direct` mode, the iterative convergence loop was skipped per workflow rules. The plan proceeds with Claude's synthesis of the draft + Codex analysis.

## Pending User Decisions

- DEC-1: Project structure approach
  - Claude Position: Single HTML file with embedded CSS/JS (simple, portable)
  - Codex Position: N/A - open question, Codex suggested considering modular structure but acknowledged single-file is valid
  - Tradeoff Summary: Single-file is simpler but harder to scale; modular is more maintainable but adds complexity. Single-file chosen to match existing project style and draft's simplicity.
  - Decision Status: `DECIDED` - Proceed with single HTML file approach

- DEC-2: Difficulty levels
  - Claude Position: Include easy/medium/hard difficulty options
  - Codex Position: N/A - open question about whether to include
  - Tradeoff Summary: More features vs. simpler core game. Added as enhancement if time permits.
  - Decision Status: `DECIDED` - Include basic difficulty (speed variation) as optional feature

## Implementation Notes

### Code Style Requirements

- Implementation code and comments must NOT contain plan-specific terminology such as "AC-", "Milestone", "Step", "Phase", or similar workflow markers
- These terms are for plan documentation only, not for the resulting codebase
- Use descriptive, domain-appropriate naming in code instead

### Standard Deliverables

Per draft requirements:
- **README.md** must be included at project root with: project title & description, prerequisites, installation steps, usage examples with code snippets, configuration options, and project structure overview
- **Git commits** must use conventional commit prefix `feat:` for all commits

--- Original Design Draft Start ---

# Requirement

帮我写一个贪吃蛇游戏

---

## Implementation Notes

- For any unspecified details (combat formulas, game balance, UI layout, tech choices, etc.), make reasonable decisions yourself and document them in the plan. Do NOT ask the user for clarification — proceed with sensible defaults.
- If referenced image files exist in the workspace, treat them as visual style references.

## Standard Deliverables (mandatory for every project)

- **README.md** — must be included at the project root with: project title & description, prerequisites, installation steps, usage examples with code snippets, configuration options, and project structure overview.
- **Git commits** — use conventional commit prefix `feat:` for all commits.

--- Original Design Draft End ---
