# System specification

## Scope and ownership

The [brief](PROJECT.md) and [design](ARCHITECTURE.md) govern the intended browser game. [DECOMPOSITION](DECOMPOSITION.md) identifies C01–C08 and applicable extensions. This specification owns observable behavior; implementation evidence is required separately. Coordinates are integer cells, x rightward and y downward, with visible columns 0–9 and rows 0–19. A cell position outside that rectangle is invalid; there are no hidden playable rows.

## B01 — Board and piece geometry

C01 supplies the seven standard tetromino types. Spawn orientation cells relative to an anchor are:

| Type | Local occupied cells |
| --- | --- |
| I | (0,1), (1,1), (2,1), (3,1) |
| J | (0,0), (0,1), (1,1), (2,1) |
| L | (2,0), (0,1), (1,1), (2,1) |
| O | (1,0), (2,0), (1,1), (2,1) |
| S | (1,0), (2,0), (0,1), (1,1) |
| T | (1,0), (0,1), (1,1), (2,1) |
| Z | (0,0), (1,0), (1,1), (2,1) |

Spawn at anchor (3,0), orientation 0. Clockwise rotation of JLSTZ local cells is (x,y) → (2−y,x); I uses (3−y,x). O remains in place. Four clockwise rotations return the original occupied cells. Each piece always has four distinct cells.

C02 owns the settled grid; an ordinary candidate is legal exactly when all four cells are inside and none overlaps a settled cell. Rejected moves leave anchor/orientation/board unchanged. Regular colors are cyan I, blue J, orange L, yellow O, green S, purple T and red Z; none is white. An outline/grid must keep settled and active cells readable against the background.

## B02 — Run lifecycle and input

Starting or restarting creates an empty board, score zero, a fresh piece source and a running active piece. Spawn failure ends the run immediately; no cells are overwritten. Game over ignores gameplay commands; restart remains available. Restart discards the old board, active state, queued input and elapsed gravity and releases any retained key state.

Left/Right move one cell, Up rotates clockwise, Down requests one-cell soft descent and R restarts. Browser repeated keydown may repeat horizontal/down movement; rotation and other one-shot actions ignore event.repeat. Handled gameplay keys prevent scrolling only while the game owns focus. Tab and native form controls retain their normal operation. On a focused setting control, arrow/Space input edits the control instead of moving/dropping a piece. A visible restart control and keyboard instructions are required.

When the document becomes hidden or focus leaves the game/its controls, suspend and clear held keys. Time, piece position and deadlines freeze. Returning focus does not resume automatically: a Resume button or Enter with game focus resumes, using a fresh wall-clock origin. Restart is allowed while suspended and begins a fresh run only when visible with game focus; otherwise the new run is suspended. Game over does not resume through Enter.

## B03 — Gravity and event ordering

C04 uses a fixed 1000 ms gravity interval, independent of frame rate and score. Each complete interval requests one downward step. A successful soft descent does not reset the scheduled gravity interval. Suspension freezes both gravity remainder and any lock remainder; resume has no hidden-time catch-up. A new active piece receives a full gravity interval.

Runtime advances elapsed active time before dispatching an input command at that time. Core processes due events in chronological order, including a lock deadline exactly equal to the event time before applying the input to the then-current piece. A single advance may cross several gravity events; the simulation must preserve their order rather than drop elapsed time. Restart cancels all previous run deadlines and stale callbacks.

## B04 — Rotation and locking

Clockwise rotation uses the unshifted candidate only. Reject it on collision or bounds failure; do not kick. A failed downward attempt, whether gravity or soft drop, immediately locks the ordinary piece. Becoming grounded after a successful step does not itself lock it; the next failed descent does. Horizontal/rotation failure does not lock. Pieces cannot pass through settled cells.

## B05 — Atomic lock, line clear and scoring

Lock requires an in-bounds non-overlapping active piece. Merge all four cells, remove every full row simultaneously, compact surviving rows downward without changing their relative order and add empty rows at the top. Increase score once by 100/300/500/800 for 1/2/3/4 cleared rows; a zero clear scores zero. There are no level multipliers or drop-distance points. Complete merge/clear/score before spawning the next piece. A blocked next spawn ends the run while retaining the completed clear and score. No frame may observe a partially merged/cleared board.

## B06 — Presentation and resource lifetime

Show board, score, lifecycle, controls, Restart and Resume when applicable. Canvas resizing/device pixel ratio changes must not change logical geometry or gameplay. Do not infer collision from pixels. Status and controls have readable DOM text/labels and visible keyboard focus. There is one runtime loop/listener set per mounted game; teardown cancels it and stale callbacks cannot affect a replacement instance. Repeated restart never adds another loop. Static play needs no account, network service, audio or local game-state storage.

## B07 — Piece source

C03 maps independent uniform random draws to I, J, L, O, S, T, Z in that order using floor(7u), u in [0,1). Tests inject deterministic random values, including values at interval boundaries. Repeated types and droughts are permitted; no bag, hold, ghost, preview, hard drop or penetrator is available.

## Q01 — Required verification

Use deterministic random streams and explicit time in core checks. Exercise each success/rejection boundary plus spawn failure, multi-row compaction, four rotations, score updates, restart, suspension and resource disposal. Browser acceptance requires isolated Chromium and Playwright-managed Firefox through the actual application runner, with keyboard interaction, form focus, Canvas/status inspection, screenshots and repeated isolated context/page teardown. Browser identity/provisioning must satisfy BROWSER_DEV_POLICY; a synthetic page proves facilities only, not application acceptance. Pin dependency versions and lockfile when implementing; unit checks cannot replace browser evidence. Do not silently drop a required browser or claim a release from document checks.

## Acceptance routes

| Contract group | Observable acceptance |
| --- | --- |
| B01–B06 | Start, translate, rotate, descend, lock, clear/score, block spawn and restart; assert exact board/score, focus/suspension and one-loop lifetime |
| B07 | Inject draws at type-interval boundaries and demonstrate repeated types without a bag |
