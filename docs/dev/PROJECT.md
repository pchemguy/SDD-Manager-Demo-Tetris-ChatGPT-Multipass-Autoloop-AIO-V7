# Browser Tetris

## Purpose and users

Provide a single-player Tetris game for desktop-browser keyboard users. Players can start immediately, see their score and controls, lose a game and restart without reloading. The application is delivered as static assets, without a backend or account.

## Product scope

Play on a 10-column, 20-row board with seven tetromino types, horizontal movement, clockwise rotation, soft drop and fixed one-second gravity. Completed rows clear simultaneously and score 100/300/500/800 points for one/two/three/four lines. A blocked spawn ends the game. Restart clears the board, score and current run.

Provide a shuffled seven-piece bag, one-use-per-piece hold, a landing ghost, SRS clockwise wall kicks and hard drop. The default locking rule waits one full gravity interval after grounding, including after hard drop. Grounded manipulation cannot repeatedly extend that deadline.

## Interaction and quality

Use TypeScript for game-state checks, Canvas for the board and ordinary DOM controls/status. Keep game rules independently testable from drawing, input and browser storage. Suspend gameplay on hidden pages or lost game focus and require deliberate resumption; suspension never advances game timers. Provide legible controls, visible keyboard focus and readable game-over/score status.

Verify deterministic game transitions and actual keyboard/rendering paths in isolated Chromium and managed Firefox environments under the repository browser policy. Headless interaction and screenshots are sufficient. The intended behavior is specified here; running software and browser compatibility require implementation evidence.

## Non-goals

Exclude multiplayer, accounts, backend leaderboards, saved games, touch controls, audio and level/speed progression. No service or network request is needed during play after static assets load. Build/dependency versions are selected and pinned during implementation; release tags are created only for verified integrated implementation phases.
