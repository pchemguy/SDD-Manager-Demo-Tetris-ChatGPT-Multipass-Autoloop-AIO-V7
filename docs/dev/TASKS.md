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
