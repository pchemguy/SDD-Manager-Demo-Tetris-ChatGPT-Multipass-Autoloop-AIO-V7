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
| C09 Landing | Pure landing projection under the applicable collision rules | Board plus candidate piece to landing cells/anchor; no draws, timers or writes | Obstacle, shaft, rotation and hard-drop agreement fixtures |

C03 owns the seven-bag queue. Draw removes one type; peek is read-only. C04 owns the held type, one-use eligibility and grounded timestamp. C01 owns ordered SRS kick offsets; C04 selects the first admissible rotation candidate against C02. C09 computes the landing once by a shared query; C07 draws the result and C04 uses it for hard drop. Empty hold draws once; swapping an occupied hold slot does not draw. Replacing an active piece creates fresh orientation and timing state.

C07 evaluates the dynamic visibility predicate over all projected cells; the query remains in C09. The predicate is independently testable and cannot influence piece movement.

C04 additionally owns bonuses and active penetration state. C09 provides ordinary/penetrator landing modes without separate hard-drop and ghost algorithms. C02 rejects any overlapping merge regardless of mode and retains settled appearance tags. C04 checks transform feasibility before spending a bonus or accepting an overlapping transit position. C07 derives white active/settled/ghost appearance and bonus indicators from the authoritative snapshot.

| Component | Responsibility and owned state | Provided / required boundary | Verification seam |
| --- | --- | --- | --- |
| C10 Configuration | Validated selected settings and defaults, independent of a run | Read values; validate setting mutation; expose per-piece lock snapshot | Domain/default tests; midgame change and restart scenarios |

C08 owns the C10 instance for the page lifetime. C04 owns each active piece's effective locking policies; C10 changes never mutate an existing timer. C06/C07 emit validated control intents through C08. C07 owns the next-piece preview and uses C03.peek without advancing the source. Hold availability combines the selected setting, the run's hold eligibility and penetration state.

| Component | Responsibility and owned state | Provided / required boundary | Verification seam |
| --- | --- | --- | --- |
| C11 Persistence | Source resolution and browser settings synchronization | Read initial URL/cookies through adapters; resolve fields through C10 codec; write one changed setting | Table-driven precedence tests and real reload/history/cookie integration |

C11 owns no game state and cannot create pieces. Its adapters expose read-cookie, write-cookie and replace-URL operations with independent failure outcomes. C10 publishes selected values only after codec validation. Startup resolves all fields before C08 creates the first run. A setting change updates memory once and attempts its cookie and URL writes separately; a failed write cannot roll back unrelated settings or trigger another run.

## Data and collaboration

The board is a row-major 20×10 settled-cell grid. Active piece data is type, clockwise orientation and integer anchor; rendering derives occupied cells through C01. Game snapshots include only observable run state, never mutable references to source queues, timers or board internals. Runtime dispatches elapsed time before an input intent at the same observed timestamp, then renders the resulting snapshot. Game processes merge, clear, score and next spawn atomically, so presentation cannot see a half-cleared board.

## Failure and lifecycle boundaries

Illegal gameplay commands are ordinary rejections. Core invariants remain enforced even if a command bypasses the UI. Browser focus loss releases tracked input and suspends the run; explicit resume starts a fresh wall-clock reference. Dispose cancels only the owned callback/listeners and makes stale callbacks inert. The random supplier is required to return finite values in [0,1); invalid test/integration suppliers fail at the source boundary rather than biasing gameplay silently. Tests may inject time and randomness but production exposes no state-editing or fixture endpoint.
