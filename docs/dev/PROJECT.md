# Browser Tetris

## Purpose and users

Provide a small, playable single-player Tetris game for people using a desktop browser and keyboard. A player can start immediately, understand the controls and score, lose a game and restart without reloading the page.

## Scope and intended outcome

The game presents a rectangular board with falling tetrominoes. Players move and rotate the active piece while gravity advances it downward. Pieces settle into the board, completed horizontal rows clear, and line clears increase the score. A blocked spawn ends the game. Restart clears the game state and begins a fresh game.

The interface shows the board, score, game-over state, keyboard instructions and a restart control. It must remain legible and responsive during play. Browser scrolling must not consume gameplay keys while the game has focus; controls must remain usable through the keyboard.

## Proposed product choices

Use a 10-column, 20-row visible board and fixed one-second gravity. Choose tetrominoes independently with equal probability. Support horizontal movement, clockwise rotation and soft drop. Reject movement or rotation that crosses a board boundary or overlaps settled cells. Lock immediately after a downward movement attempt fails. Score single, double, triple and four-line clears as 100, 300, 500 and 800 points respectively, without a level multiplier or drop-distance points.

Suspend simulation when the page is hidden or game focus is lost and require deliberate resumption, avoiding an unexpected loss while the player is away. Restart discards the current run and resets score, board and piece state.

Deliver a static browser application without a server-side service. TypeScript with a Canvas board and ordinary DOM status/controls is the recommended implementation direction: it keeps drawing and controls simple while supporting checked game-state transitions. Exact build tooling, controls and behavioral acceptance fixtures will be defined in the design and specification.

## Non-goals

The product excludes multiplayer, accounts, leaderboards, saved game state, mobile touch controls, audio, level progression and adjustable settings. It includes no hold, landing ghost, next-piece preview, bag randomizer, wall kicks, hard drop or penetration ability.

## Quality and verification

Keep game rules independently testable from drawing and browser input. Verify board transitions, scoring, spawn failure and restart with deterministic scenarios. Exercise actual keyboard interaction and rendered board output in isolated Chromium and managed Firefox environments under the repository browser policy. Headless execution is sufficient for those checks. Browser installation and application execution remain unverified at this documentation stage.

These product choices are proposals awaiting acceptance; the requested core gameplay is retained without unresolved contradictions. The intended first playable version is v0.1.0.
