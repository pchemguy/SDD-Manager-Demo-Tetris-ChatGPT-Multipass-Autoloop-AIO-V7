# Architecture

## Context and arrangement

The [project brief](PROJECT.md) defines a static desktop-browser game. A deterministic rules core owns gameplay. A browser runtime translates input and elapsed time into commands and draws immutable snapshots. The core neither reads the DOM nor schedules its own callbacks. This permits deterministic checks without a browser and keeps frame rate separate from game time.

| Block | Owns | Dependencies and boundary |
| --- | --- | --- |
| Rules core | Board, active piece, score, lifecycle and legal state transitions | Geometry and injected random source; no browser globals, timers or rendering |
| Runtime controller | One game instance, animation callback, focus/suspension and command ordering | Rules core and browser adapters; the single place that dispatches commands/time |
| Presentation | Canvas board and DOM controls/status | Read-only snapshot and callbacks to runtime; cannot mutate gameplay |
| Browser input | Keyboard/focus events and control intents | Runtime command boundary; does not run rules or retain a second board |
| Verification harness | Seeded draws, explicit timestamps and browser fixtures | Public core/controller boundaries; no production debug backdoor |

Dependencies point from browser adapters into the core. Types shared across a boundary are plain data; internal ownership remains with one component. Avoid inheritance trees, a general event bus, plugin registries and duplicate state stores: the product has one board and one local session, so these mechanisms add little value.

## State and lifecycle

The core owns the settled grid, active piece, source state, score and lifecycle (`running`, `suspended`, `gameOver`). Runtime owns scheduling and physical focus; it passes suspension/resumption commands so core time cannot advance while inactive. Restart constructs a fresh run, releases prior input state and invalidates old callbacks. There is exactly one animation loop and one set of listeners; teardown cancels/removes all owned resources.

Presentation receives copied/read-only snapshots. Drawn pixels are never collision input. Random draws and explicit elapsed time are injected; renderer calls cannot advance a source or mutate a timer. Rejected commands leave the run unchanged except for elapsed time processed before their timestamp. Internal invariant failures are programming errors surfaced by tests; they are not repaired by silently deleting settled cells.

## Verification and tradeoffs

Canvas keeps board drawing simple; DOM controls provide semantic form interaction and readable status. Pure transitions trade a small amount of snapshot copying for clear ownership and deterministic testing; the board is only 200 cells. Tests use public commands and snapshots rather than reproducing implementation algorithms. Browser verification covers focus, keyboard routing, Canvas output and teardown in both required browsers. Provisioning follows the root browser policy; document readiness does not establish runtime capability.

The component model in DECOMPOSITION defines the logical seams. SPEC owns exact behavior, PLAN delivery boundaries and layout physical allocation.
