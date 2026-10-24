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

## Piece lifecycle and projections

The piece source owns a shuffled bag and provides draw/peek semantics without exposing its queue for mutation. Game owns hold eligibility, active-piece replacement and the lock deadline. A shared landing query produces a projection from board and candidate piece; ghost and hard drop consume the same result. Timing is integrated inside Game using explicit event times, while Runtime owns wall-clock observation. This keeps a grounded deadline consistent across frames, input and suspension.

Rotation uses canonical shape states and an ordered kick table. Geometry tests isolate pivots/offsets; Game tests integrate collision, hold, landing and timing. Hold swaps a type through Game rather than exchanging a mutable active-piece object.

Ghost visibility is a separate decision over the computed projection. Hiding a projection does not change its geometry or consume randomness. Both midline boundaries and rendering can therefore be verified without duplicating landing logic.

## Penetration policy

Game owns the bonus inventory and the active piece's penetration flag. The landing query selects an ordinary or penetrator collision policy. Both policies retain board bounds; penetration permits transit overlap but never an overlapping lock. Game validates future landing feasibility after candidate transformations. Settled cells carry an appearance tag so a locked white penetrator remains white without retaining active ability. No block is deleted to make a landing possible.

The renderer distinguishes ghost/active/settled layers while respecting the white/non-white color rule. Bonus symbols and accessible count derive from the same inventory snapshot, preventing a separately updated UI counter.

## Configuration boundary

Configuration owns validated selected settings independently of a run. Runtime applies immediate display/action availability values and supplies a snapshot of locking policies when Game creates each active piece. Game retains the effective per-piece timing snapshot; presentation may show selected and effective policy without leaking internal implementation. Restart resets gameplay while retaining selected settings. Control changes are validated before dispatch, and no input handler edits configuration or gameplay fields directly.

The configuration adapter is in-memory. Reload creates a new default configuration; the application has no storage or URL synchronization side effects.

## Verification and tradeoffs

Canvas keeps board drawing simple; DOM controls provide semantic form interaction and readable status. Pure transitions trade a small amount of snapshot copying for clear ownership and deterministic testing; the board is only 200 cells. Tests use public commands and snapshots rather than reproducing implementation algorithms. Browser verification covers focus, keyboard routing, Canvas output and teardown in both required browsers. Provisioning follows the root browser policy; document readiness does not establish runtime capability.

The [component model](DECOMPOSITION.md) defines the logical seams. SPEC owns exact behavior, PLAN delivery boundaries and layout physical allocation.
