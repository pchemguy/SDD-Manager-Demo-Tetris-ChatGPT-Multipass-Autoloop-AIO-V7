# Component model

The [architecture](ARCHITECTURE.md) separates a rules core from browser scheduling and presentation. Interfaces below describe responsibility and state ownership; SPEC defines observable contracts. Each component has one reason to change and a focused verification seam.

| Component | Responsibility and owned state | Provided / required boundary | Verification seam |
| --- | --- | --- | --- |
| C01 Geometry | Tetromino cell states, rotation candidates and board coordinates | Cells for a type/orientation/anchor; no board mutation or random draws | Canonical shape/pivot and boundary fixtures |
| C02 Board | Settled cells, placement legality, atomic merge/clear and compaction | Read collision/cells; merge legal cells; return cleared-row count | Empty/occupied bounds, simultaneous clears, stable row order |
| C03 PieceSource | Random selection state | Draw next type using injected random supplier; restart source lifecycle | Controlled random stream and draw sequence assertions |
| C04 Game | Run lifecycle, active piece, score and command/time transitions | New run; dispatch command; advance explicit duration; read snapshot | Deterministic command/time scenarios without DOM |
| C05 RuntimeClock | Last active timestamp, callback ownership and suspension routing | Translate monotonic wall time into Game time; schedule/cancel | Fake scheduler and exact elapsed-time assertions |
| C06 Input | Press/release tracking and semantic command mapping | Forward supported intent to Runtime; suppress only handled gameplay defaults | Real key/focus tests plus pure mapping checks |
| C07 View | Canvas rasterization and DOM status/control bindings | Render snapshot; emit control intent; no Game writes | Snapshot-driven Canvas pixels and DOM/focus assertions |
| C08 Runtime | Composition, command ordering and one application lifetime | Construct/dispose collaborators; own their subscriptions | Repeated mount/suspend/resume/dispose integration |

## Data and collaboration

The board is a row-major 20×10 settled-cell grid. Active piece data is type, clockwise orientation and integer anchor; rendering derives occupied cells through C01. Game snapshots include only observable run state, never mutable references to source queues, timers or board internals. Runtime dispatches elapsed time before an input intent at the same observed timestamp, then renders the resulting snapshot. Game processes merge, clear, score and next spawn atomically, so presentation cannot see a half-cleared board.

## Failure and lifecycle boundaries

Illegal gameplay commands are ordinary rejections. Core invariants remain enforced even if a command bypasses the UI. Browser focus loss releases tracked input and suspends the run; explicit resume starts a fresh wall-clock reference. Dispose cancels only the owned callback/listeners and makes stale callbacks inert. The random supplier is required to return finite values in [0,1); invalid test/integration suppliers fail at the source boundary rather than biasing gameplay silently. Tests may inject time and randomness but production exposes no state-editing or fixture endpoint.
