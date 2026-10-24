# Implementation tasks

This list derives from [SPEC](SPEC.md), [PLAN](PLAN.md), [DECOMPOSITION](DECOMPOSITION.md) and [layout](layout.md). It records intended executable work; all implementation tasks start unchecked. Each task includes its own meaningful tests and documentation. Preserve one task’s result, evidence and initial owning checkbox in one commit, then push/read back and reconcile its issue before dependent work. Exact versions and executable commands are established by the setup task, not claimed here.

Each phase’s final milestone has exactly one phase review task. Delivery milestones below have fewer than four implementation tasks, so their final implementation task owns whole-milestone review/testing/repair/report and HANDOFF; no standalone milestone review task is added. Reports distinguish blockers from eligible non-critical TODOs. Implementation ranges, phase activation, integration and releases remain subject to SDD Manager and PLAN gates.

## Phase 1 — Playable classic baseline

- [ ] Phase 1 — Playable classic baseline
    - [ ] Milestone 1.1 — Falling-piece slice
        - [ ] T-001 — Establish the static build and isolated verification harness
            Scope: package.json, lockfile, TypeScript/Vite/Vitest/Playwright configuration and browser setup documentation. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: none.
            Evidence: Pin supported tool/dependency versions; typecheck, unit runner and static build execute. Provision isolated Chromium and managed Firefox under BROWSER_DEV_POLICY and demonstrate bounded repeated context/page/interaction/render/teardown through the selected runner before dependent browser checks.
        - [ ] T-002 — Define tetromino geometry and settled-board operations
            Scope: src/core/geometry.ts, src/core/board.ts and focused tests. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-001.
            Evidence: Check all spawn cells, four rotations, bounds/collision and row representation under B01. Use controlled fixtures; reject invalid candidates without mutation.
        - [ ] T-003 — Integrate the falling-piece keyboard and Canvas slice
            Scope: src/core/game.ts, source.ts, src/browser/runtime.ts, clock.ts, input.ts, view.ts and integration tests. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-001, T-002.
            Evidence: Show a piece falling at fixed gravity with Left/Right/Up/Down, ordinary collision rejection and visible score/controls. Time and source injection are testable; no future gameplay capability is introduced.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/1/1.1.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 1.2 — Complete classic run lifecycle
        - [ ] T-004 — Implement atomic settlement, compaction and scoring
            Scope: src/core/board.ts, game.ts and transition fixtures. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-003.
            Evidence: Lock only on failed descent, merge four legal cells, clear simultaneous full rows, retain row order and apply exact 100/300/500/800 scores without drop points.
        - [ ] T-005 — Complete blocked-spawn game over and fresh restart
            Scope: src/core/game.ts, src/browser/view.ts, input.ts and lifecycle tests. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-004.
            Evidence: Blocked spawn preserves the settled board/score; game over ignores movement, restart clears run/source/timers and works repeatedly without additional listeners.
        - [ ] T-006 — Integrate suspension, focus and resource disposal
            Scope: src/browser/runtime.ts, clock.ts, input.ts, view.ts and browser checks. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-004, T-005.
            Evidence: Lose focus/hide, freeze timers and keys, explicitly resume without catch-up; native controls/Tab work and repeated restart/dispose leaves one loop. Verify the whole classic run lifecycle.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/1/1.2.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 1.3 — Verified static delivery
        - [ ] T-007 — Complete deterministic classic boundary coverage
            Scope: tests/unit and tests/integration fixtures for core/runtime. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-006.
            Evidence: Cover shape/source boundaries, collision rejections, score/compaction, blocked spawn, restart and exact elapsed-time ordering without duplicating production algorithms.
        - [ ] T-008 — Verify actual cross-browser gameplay and rendering
            Scope: tests/e2e, owned screenshots and browser evidence. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-007.
            Evidence: Run the real built/served app in Chromium and managed Firefox; exercise keyboard/focus, line-clear/score, game-over/restart, suspension, visible Canvas and repeated isolated teardown. Missing required browser evidence blocks acceptance.
        - [ ] T-009 — Prepare classic user guidance and static release package
            Scope: README.md, docs/user, package metadata and RELEASE-NOTES.md. Contracts: B01–B07, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-007, T-008.
            Evidence: Document validated install/run/check commands and controls, build static assets, set v0.1.0 and prepare notes matching delivered baseline. Do not publish a release until phase review/integration. Verify whole delivery milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/1/1.3.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 1.4 — Phase review
        - [ ] T-010 — Review, test and report phase 1
            Scope: whole phase implementation, integration boundaries, scoped PLAN exits, reports and carried findings. Depends on: T-003, T-006, T-009 and verified completion/closure of delivery milestones 1.1, 1.2, 1.3.
            Evidence: separate code review and required type/unit/integration/browser/build evidence; repair blockers, retain `docs/dev/reports/phases/1/PHASE-REPORT.md` and HANDOFF with initial completion. Aggregate unresolved milestone TODOs with evidence/rationale/options/owners. If this is the final phase of the complete intended list, include `docs/dev/reports/IMPLEMENTATION-REPORT.md` and final TODO aggregation. Do not claim release publication before verified integration/tag/release operations.

## Phase 2 — Gameplay enhancements

- [ ] Phase 2 — Gameplay enhancements
    - [ ] Milestone 2.1 — Bag and held-piece lifecycle
        - [ ] T-011 — Implement seven-bag draws and pure peek
            Scope: src/core/source.ts and source fixtures. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-010. Predecessor phase must also be integrated/published and its milestone closures verified.
            Evidence: Each aligned bag contains every type once; seeded order is reproducible, bag boundaries and peek do not consume extra types.
        - [ ] T-012 — Implement hold replacement and eligibility
            Scope: src/core/game.ts and hold fixtures. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-011.
            Evidence: Empty hold draws once, populated swap draws none, replacement resets spawn/orientation/time, repeated use rejects and blocked replacement ends the run.
        - [ ] T-013 — Integrate held-piece display and input
            Scope: src/browser/input.ts, view.ts and integration/e2e checks. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-011, T-012.
            Evidence: C/hold control works once per piece, held type is visible, restart clears it and queue/state remain consistent through locks. Verify whole bag/hold milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/2/2.1.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 2.2 — Rotation and grounded drop lifecycle
        - [ ] T-014 — Implement ordered clockwise SRS wall kicks
            Scope: src/core/geometry.ts, game.ts, tests/fixtures/rotation and unit tests. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-013.
            Evidence: Use SPEC rotation tables for every JLSTZ/I transition, O invariance, first-success ordering and all-candidate rejection.
        - [ ] T-015 — Implement full-interval grounded locking
            Scope: src/core/game.ts and explicit-time fixtures. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-014.
            Evidence: At 999 ms grounded retain active piece; at 1000 ms lock; failed moves/repeated grounded actions do not extend it, airborne transition cancels it and suspension freezes it.
        - [ ] T-016 — Integrate hard drop with shared landing and timing
            Scope: src/core/landing.ts, game.ts, src/browser/input.ts and integration tests. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-014, T-015.
            Evidence: Space moves to ordinary first-barrier landing, adds no score, starts/retains grounding as applicable and never locks immediately by default. Verify rotation/timing/drop interaction and entire milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/2/2.2.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 2.3 — Ghost and composed enhancement delivery
        - [ ] T-017 — Render the shared landing ghost
            Scope: src/browser/view.ts, src/core/landing.ts and visual checks. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-016.
            Evidence: Ghost uses the hard-drop query for active type/orientation, remains distinguishable under the active piece and never mutates source/board.
        - [ ] T-018 — Verify enhancement lifecycle interactions
            Scope: tests/unit, tests/integration and tests/e2e scenarios. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-017.
            Evidence: Compose hold, bag, wall kicks, projection, hard drop, restart and suspended deadlines; check source conservation and unchanged scoring/spawn failure.
        - [ ] T-019 — Prepare enhanced browser delivery and guidance
            Scope: tests/e2e, docs/user, README.md, version metadata and RELEASE-NOTES.md. Contracts: E01–E02, B04, Q01; preserved base gameplay, narrowed to this phase’s PLAN scope.
            Depends on: T-017, T-018.
            Evidence: Run both required browsers, inspect ghost/hold output and controls, build assets, prepare v0.2.0 notes and document timer behavior. Verify whole composed milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/2/2.3.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 2.4 — Phase review
        - [ ] T-020 — Review, test and report phase 2
            Scope: whole phase implementation, integration boundaries, scoped PLAN exits, reports and carried findings. Depends on: T-013, T-016, T-019 and verified completion/closure of delivery milestones 2.1, 2.2, 2.3.
            Evidence: separate code review and required type/unit/integration/browser/build evidence; repair blockers, retain `docs/dev/reports/phases/2/PHASE-REPORT.md` and HANDOFF with initial completion. Aggregate unresolved milestone TODOs with evidence/rationale/options/owners. If this is the final phase of the complete intended list, include `docs/dev/reports/IMPLEMENTATION-REPORT.md` and final TODO aggregation. Do not claim release publication before verified integration/tag/release operations.

## Phase 3 — Conditional ghost visibility

- [ ] Phase 3 — Conditional ghost visibility
    - [ ] Milestone 3.1 — Dynamic projection visibility
        - [ ] T-021 — Apply the whole-projection midline predicate
            Scope: src/browser/view.ts and focused unit/visual fixtures. Contracts: V01, E02, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-020. Predecessor phase must also be integrated/published and its milestone closures verified.
            Evidence: min projected y ≥ 10 shows; min y 9 and straddling cells hide. Test active piece above a lower projection; do not change landing/source/timers.
        - [ ] T-022 — Verify and document dynamic ghost delivery
            Scope: tests/e2e, docs/user, version metadata and RELEASE-NOTES.md. Contracts: V01, E02, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-021.
            Evidence: In both browsers exercise boundary/rotation/reappearance and hidden-ghost hard drop; run enhanced regressions and static build, prepare v0.3.0 notes. Verify whole visibility milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/3/3.1.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 3.2 — Phase review
        - [ ] T-023 — Review, test and report phase 3
            Scope: whole phase implementation, integration boundaries, scoped PLAN exits, reports and carried findings. Depends on: T-022 and verified completion/closure of delivery milestones 3.1.
            Evidence: separate code review and required type/unit/integration/browser/build evidence; repair blockers, retain `docs/dev/reports/phases/3/PHASE-REPORT.md` and HANDOFF with initial completion. Aggregate unresolved milestone TODOs with evidence/rationale/options/owners. If this is the final phase of the complete intended list, include `docs/dev/reports/IMPLEMENTATION-REPORT.md` and final TODO aggregation. Do not claim release publication before verified integration/tag/release operations.

## Phase 4 — Penetrator mode

- [ ] Phase 4 — Penetrator mode
    - [ ] Milestone 4.1 — Safe penetration movement
        - [ ] T-024 — Define the deepest-valid penetrator landing query
            Scope: src/core/landing.ts and board/landing fixtures. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-023. Predecessor phase must also be integrated/published and its milestone closures verified.
            Evidence: Enumerate in-bounds non-overlapping lower anchors irrespective of intervening occupancy; ordinary projection still stops at the first barrier. Check absent and zero-distance landings.
        - [ ] T-025 — Integrate penetrator traversal and transform feasibility
            Scope: src/core/game.ts, geometry/landing boundaries and unit tests. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-024.
            Evidence: Gravity/soft descent allow transient overlap only within bounds and toward a feasible target; lateral/rotation candidates require a valid landing at/below current y; reject stranded changes.
        - [ ] T-026 — Integrate legal penetration lock, hard drop and ghost
            Scope: src/core/game.ts, landing.ts, src/browser/view.ts and integration tests. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-024, T-025.
            Evidence: Use the same target for gravity/drop/ghost, start lock timing only at a legal landing and never merge overlapping cells. Verify all movement/timer transitions and whole safety milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/4/4.1.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 4.2 — Bonus activation and readable feedback
        - [ ] T-027 — Award and cap penetrator bonuses
            Scope: src/core/game.ts and atomic-clear fixtures. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-026.
            Evidence: Every four-line clear awards one up to three, other counts none, both piece modes qualify, restart clears inventory and blocked next spawn retains earned results.
        - [ ] T-028 — Gate activation, spending and hold lifecycle
            Scope: src/core/game.ts, src/browser/input.ts and lifecycle fixtures. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-027.
            Evidence: B spends once only after feasibility, repeated/empty/infeasible activation rejects, hold is disabled while active and ability ends on lock/game over. Activation does not extend an existing grounded deadline.
        - [ ] T-029 — Render white penetrators and exact bonus indicators
            Scope: src/browser/view.ts, styles and visual/e2e fixtures. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-027, T-028.
            Evidence: Active/settled penetrators are white; regular palette is non-white. Distinct white ghost obeys midline; symbols and numeric count match 0–3 after earning/spending. Verify whole activation/feedback milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/4/4.2.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 4.3 — Composed penetrator delivery
        - [ ] T-030 — Complete penetrator boundary and interaction fixtures
            Scope: tests/unit, tests/integration and tests/fixtures/penetration. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-029.
            Evidence: Cover multiple cavities, rotation feasibility, overlapping transit, cap/spend/award, both spawn-failure and hold gates, suspension and timer preservation without a production fixture backdoor.
        - [ ] T-031 — Verify penetrator browser interaction and rendering
            Scope: tests/e2e and owned rendering evidence. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-030.
            Evidence: Exercise real B/Space/C input, inventory/white cells, dynamic ghost and preserved settled barriers in both required browsers; regress ordinary game behavior.
        - [ ] T-032 — Prepare penetrator guidance and package
            Scope: docs/user, README.md, version metadata and RELEASE-NOTES.md. Contracts: P01–P02, E01–E02, V01, Q01, narrowed to this phase’s PLAN scope.
            Depends on: T-030, T-031.
            Evidence: Document activation/bonuses/hold restriction/landing behavior; build static assets, prepare v0.4.0 notes and verify whole composed milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/4/4.3.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 4.4 — Phase review
        - [ ] T-033 — Review, test and report phase 4
            Scope: whole phase implementation, integration boundaries, scoped PLAN exits, reports and carried findings. Depends on: T-026, T-029, T-032 and verified completion/closure of delivery milestones 4.1, 4.2, 4.3.
            Evidence: separate code review and required type/unit/integration/browser/build evidence; repair blockers, retain `docs/dev/reports/phases/4/PHASE-REPORT.md` and HANDOFF with initial completion. Aggregate unresolved milestone TODOs with evidence/rationale/options/owners. If this is the final phase of the complete intended list, include `docs/dev/reports/IMPLEMENTATION-REPORT.md` and final TODO aggregation. Do not claim release publication before verified integration/tag/release operations.

## Phase 5 — Session-only configuration

- [ ] Phase 5 — Session-only configuration
    - [ ] Milestone 5.1 — Configuration and effective locking
        - [ ] T-034 — Define validated session configuration state
            Scope: src/config/settings.ts, codec.ts and domain/default tests. Contracts: C01, configuration session boundary, preserved P/V/E/B contracts, narrowed to this phase’s PLAN scope.
            Depends on: T-033. Predecessor phase must also be integrated/published and its milestone closures verified.
            Evidence: All six domains/defaults match CONFIGURATION; reject invalid intents, retain values over restart and use no persistence source or sink.
        - [ ] T-035 — Apply per-piece general and hard-drop locking policies
            Scope: src/core/game.ts, src/browser/runtime.ts and timing fixtures. Contracts: C01, configuration session boundary, preserved P/V/E/B contracts, narrowed to this phase’s PLAN scope.
            Depends on: T-034.
            Evidence: Spawn/hold replacement snapshots policies; failed descent locks only at a valid landing, interval timing remains unchanged and immediate hard drop locks synchronously only when enabled.
        - [ ] T-036 — Integrate labeled configuration controls and live gates
            Scope: src/browser/view.ts, input.ts, runtime.ts and browser checks. Contracts: C01, configuration session boundary, preserved P/V/E/B contracts, narrowed to this phase’s PLAN scope.
            Depends on: T-034, T-035.
            Evidence: Native controls preserve keyboard focus, immediate toggles do not reset timers/hold eligibility, selected lock changes affect next piece and penetration still blocks hold. Verify whole configuration/locking milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/5/5.1.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 5.2 — Preview and session delivery
        - [ ] T-037 — Integrate pure next-piece preview
            Scope: src/browser/view.ts, src/core/source.ts and source/UI fixtures. Contracts: C01, configuration session boundary, preserved P/V/E/B contracts, narrowed to this phase’s PLAN scope.
            Depends on: T-036.
            Evidence: Display the next type in spawn orientation, hide without drawing, advance after lock/empty hold and remain stable on occupied hold swap; regular colors are non-white.
        - [ ] T-038 — Verify session settings and gameplay interaction matrix
            Scope: tests/e2e and unit/integration coverage. Contracts: C01, configuration session boundary, preserved P/V/E/B contracts, narrowed to this phase’s PLAN scope.
            Depends on: T-037.
            Evidence: Exercise all values, both lock settings combinations, hard-drop off, hold gates, ghost modes, paused changes, next preview, restart retention and reload defaults even with settings-like URL/cookies. Verify no storage/history side effects in both browsers.
        - [ ] T-039 — Prepare configuration guidance and static package
            Scope: docs/user, README.md, version metadata and RELEASE-NOTES.md. Contracts: C01, configuration session boundary, preserved P/V/E/B contracts, narrowed to this phase’s PLAN scope.
            Depends on: T-037, T-038.
            Evidence: Document defaults, per-piece timing adoption, live controls and session-only lifetime; build static assets, prepare v0.5.0 notes and verify whole preview/session milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/5/5.2.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 5.3 — Phase review
        - [ ] T-040 — Review, test and report phase 5
            Scope: whole phase implementation, integration boundaries, scoped PLAN exits, reports and carried findings. Depends on: T-036, T-039 and verified completion/closure of delivery milestones 5.1, 5.2.
            Evidence: separate code review and required type/unit/integration/browser/build evidence; repair blockers, retain `docs/dev/reports/phases/5/PHASE-REPORT.md` and HANDOFF with initial completion. Aggregate unresolved milestone TODOs with evidence/rationale/options/owners. If this is the final phase of the complete intended list, include `docs/dev/reports/IMPLEMENTATION-REPORT.md` and final TODO aggregation. Do not claim release publication before verified integration/tag/release operations.

## Phase 6 — Configuration persistence

- [ ] Phase 6 — Configuration persistence
    - [ ] Milestone 6.1 — Validated restoration before play
        - [ ] T-041 — Define external schema parsing and independent resolution
            Scope: src/config/codec.ts, persistence.ts and pure source fixtures. Contracts: C02 and CONFIGURATION persistence schema; preserved C01 gameplay timing, narrowed to this phase’s PLAN scope.
            Depends on: T-040. Predecessor phase must also be integrated/published and its milestone closures verified.
            Evidence: Exact case-sensitive names/values; malformed/empty/duplicate recognized sources fall through per field. Valid explicit URL defaults win and omissions preserve cookies.
        - [ ] T-042 — Implement protected settings-cookie access
            Scope: src/config/browser-storage.ts and adapter/integration tests. Contracts: C02 and CONFIGURATION persistence schema; preserved C01 gameplay timing, narrowed to this phase’s PLAN scope.
            Depends on: T-041.
            Evidence: Read/write only tetris.<key> cookies with exact lifetime/path/samesite/HTTPS attributes, preserve other cookies and retain memory on blocked access/readback failure.
        - [ ] T-043 — Integrate startup restoration and explicit URL cookie saves
            Scope: src/config/persistence.ts, src/browser/runtime.ts and bootstrap tests. Contracts: C02 and CONFIGURATION persistence schema; preserved C01 gameplay timing, narrowed to this phase’s PLAN scope.
            Depends on: T-041, T-042.
            Evidence: Resolve before first spawn, save every valid explicit URL field including defaults, never overwrite omitted/invalid fields and allow remaining sources when one read channel fails. Verify whole restoration milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/6/6.1.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 6.2 — Synchronized edits and durable delivery
        - [ ] T-044 — Synchronize query edits and independent save outcomes
            Scope: src/config/browser-storage.ts, persistence.ts, runtime.ts and integration tests. Contracts: C02 and CONFIGURATION persistence schema; preserved C01 gameplay timing, narrowed to this phase’s PLAN scope.
            Depends on: T-043.
            Evidence: Replace only the edited query setting with history.replaceState, preserve unrelated parameters/fragment semantically and attempt cookie/history writes independently, including same-value edits; no recursion/navigation.
        - [ ] T-045 — Verify reload, precedence and channel-failure scenarios
            Scope: tests/e2e, tests/unit and tests/integration fixtures. Contracts: C02 and CONFIGURATION persistence schema; preserved C01 gameplay timing, narrowed to this phase’s PLAN scope.
            Depends on: T-044.
            Evidence: In both browsers run mixed sources, explicit defaults, omissions, invalid/duplicate values, isolated control edits, cookie/history/both failures, restart and actual reload. Gameplay configuration timing remains unchanged.
        - [ ] T-046 — Prepare durable-settings guidance and package
            Scope: docs/user, README.md, version metadata and RELEASE-NOTES.md. Contracts: C02 and CONFIGURATION persistence schema; preserved C01 gameplay timing, narrowed to this phase’s PLAN scope.
            Depends on: T-044, T-045.
            Evidence: Document names/domains/precedence, one-origin cookie namespace, blocked-channel limits and reload behavior. Build assets, prepare v0.6.0 notes and verify whole synchronization milestone.
            Milestone boundary: after this implementation and all prior milestone tasks, review the whole capability’s code/dependencies, execute required acceptance/regressions, repair blockers and commit report `docs/dev/reports/phases/6/6.2.md` plus HANDOFF with this task’s result and initial checkbox. Include findings and TODOs (None when empty); close/read back all task issues before closing the milestone.
    - [ ] Milestone 6.3 — Phase review
        - [ ] T-047 — Review, test and report phase 6
            Scope: whole phase implementation, integration boundaries, scoped PLAN exits, reports and carried findings. Depends on: T-043, T-046 and verified completion/closure of delivery milestones 6.1, 6.2.
            Evidence: separate code review and required type/unit/integration/browser/build evidence; repair blockers, retain `docs/dev/reports/phases/6/PHASE-REPORT.md` and HANDOFF with initial completion. Aggregate unresolved milestone TODOs with evidence/rationale/options/owners. If this is the final phase of the complete intended list, include `docs/dev/reports/IMPLEMENTATION-REPORT.md` and final TODO aggregation. Do not claim release publication before verified integration/tag/release operations.
