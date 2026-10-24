# Delivery plan

## Strategy and delivery controls

Deliver useful functionality in bounded phases, preserving each preceding playable outcome. [SPEC](SPEC.md) owns the complete current behavior; phase exits below intentionally narrow verification to each delivered capability and its regressions. Do not treat later requirements as prerequisites for the simplest playable classic game. The [component model](DECOMPOSITION.md) guides cohesive work; TASKS supplies executable units and layout physical ownership.

Each delivery milestone has integrated demonstration, code review, relevant tests, blocker repair and a committed report/HANDOFF. TASKS adds a standalone milestone review task only when there are at least four implementation tasks in that milestone and at least two implementation milestones in its phase; otherwise the final implementation task owns the complete milestone boundary. Every phase retains a separate final single-task phase review milestone. Counts do not justify artificial scope or padding.

Implementation requires separately authorized task ranges and verified document integration. Project tracking activates only the eligible implementation phase, including all its milestones/tasks; future phases remain unprojected. Close verified task issues after their atomic result/evidence/checkbox commit is pushed/read back; close delivery milestones before phase review. Incomplete phases remain on their working branch. A completed verified phase explicitly integrates into its recorded target before dependent phase work.

## Verification, packaging and releases

Use deterministic core checks plus actual application interaction/rendering in isolated Chromium and managed Firefox. Browser provisioning follows BROWSER_DEV_POLICY, including proactive diagnostics and supported recovery before declaring dependent work blocked. Do not install browsers for documentation preparation or substitute unit checks for browser acceptance. Pin TypeScript/Vite/Vitest/Playwright and their lockfile when implementing; proposed checks are typecheck, unit/integration, static build and Playwright application tests.

Each phase includes user/developer guidance, version metadata, reproducible static packaging and scoped release-note preparation. The first playable release is v0.1.0; additive phases increment the minor version and verified repairs increment patch versions. Publish one GitHub release after each authorized implementation phase is complete, verified and integrated. Release tags target verified release commits on actual default branch main; notes identify delivered behavior, checks and material limitations. Preparation documents alone create no release.

## Risks and exit discipline

Keep time/randomness injectable, test collision/lock rejection boundaries and inspect visible Canvas output. Required browser or publication failures block the affected claim/transition; preserve work and investigate supported alternatives without silently dropping requirements. Fix bugs and SPEC/PLAN violations before boundary completion. Only non-critical code findings that preserve contracts may be deferred with severity/evidence/rationale/options/owner in report TODOs. Phase reports retain milestone findings; the final phase review aggregates unresolved/deferred TODOs without losing provenance.

## Phase 1 — Playable classic baseline

Outcome and included scope: Classic movement, gravity, immediate failed-descent locking, simultaneous line clear/scoring, game over, restart and focus suspension. Independent random types, unshifted clockwise rotation, fixed speed; no hold, ghost, bag, kicks, hard drop, penetration or settings.

Dependency: None; initial usable product.

Contracts: B01–B07, Q01. Target release: v0.1.0.

### Milestone 1.1 — Falling-piece slice

A real board displays a falling, movable and rotatable tetromino; demonstrate responsiveness and legibility before settlement work.

Exit: demonstrate this integrated capability, review its code and relevant dependencies, run focused acceptance/regressions, repair blockers and retain a milestone report/HANDOFF. TASKS assigns these obligations to the appropriate final boundary task under the review-unit policy. Feedback may support a human decision to continue, amend, simplify or stop; it does not automatically change authorized scope.

### Milestone 1.2 — Complete classic run lifecycle

Play continuously through settlement, scored row clear, loss and restart; demonstrate interruption/resumption without surprise motion.

Exit: demonstrate this integrated capability, review its code and relevant dependencies, run focused acceptance/regressions, repair blockers and retain a milestone report/HANDOFF. TASKS assigns these obligations to the appropriate final boundary task under the review-unit policy. Feedback may support a human decision to continue, amend, simplify or stop; it does not automatically change authorized scope.

### Milestone 1.3 — Verified static delivery

Demonstrate the built application and readable controls in both browsers; use failures/screenshots to decide readiness before phase integration.

Exit: demonstrate this integrated capability, review its code and relevant dependencies, run focused acceptance/regressions, repair blockers and retain a milestone report/HANDOFF. TASKS assigns these obligations to the appropriate final boundary task under the review-unit policy. Feedback may support a human decision to continue, amend, simplify or stop; it does not automatically change authorized scope.

### Milestone 1.4 — Phase review

Exactly one phase code-review/testing/report outcome after every delivery milestone is verified and closed. Verify cross-milestone behavior, the phase exits below and carried findings; repair blockers, retain the phase report and aggregate deferred TODOs. When this is the final phase of the complete intended task list, also retain the final implementation report/TODO aggregation. This special review milestone is not a delivery-count target.

Phase exits: Demonstrate a real keyboard-controlled game through line clear, spawn failure and restart. Verify fixed timing, immediate failed-descent lock, score, bounds, focus/resume and clean teardown in Chromium/Firefox. Produce static build, controls/setup documentation and scoped release notes.

Integration/release boundary: complete all phase tasks/reports and applicable hosted closures, explicitly integrate into the recorded target, verify the merged build and relevant regressions, publish/read back the default-branch release commit/tag, then publish release notes for v0.1.0. A partial phase stops on its working branch. No later capability is required for this phase’s scoped exit.

## Phase 2 — Gameplay enhancements

Outcome and included scope: Seven-bag source, hold, SRS clockwise wall kicks, full-interval grounding deadline, hard drop and always-visible landing ghost. Keep settings/preview/penetration absent.

Dependency: Phase 1 verified, integrated and published.

Contracts: E01–E02, B04, Q01; preserved base gameplay. Target release: v0.2.0.

### Milestone 2.1 — Bag and held-piece lifecycle

Demonstrate controlled bag order and one-use hold through consecutive locks without losing a usable game.

Exit: demonstrate this integrated capability, review its code and relevant dependencies, run focused acceptance/regressions, repair blockers and retain a milestone report/HANDOFF. TASKS assigns these obligations to the appropriate final boundary task under the review-unit policy. Feedback may support a human decision to continue, amend, simplify or stop; it does not automatically change authorized scope.

### Milestone 2.2 — Rotation and grounded drop lifecycle

Demonstrate first-valid SRS candidate selection and hard drop that preserves a non-resetting grounded deadline.

Exit: demonstrate this integrated capability, review its code and relevant dependencies, run focused acceptance/regressions, repair blockers and retain a milestone report/HANDOFF. TASKS assigns these obligations to the appropriate final boundary task under the review-unit policy. Feedback may support a human decision to continue, amend, simplify or stop; it does not automatically change authorized scope.

### Milestone 2.3 — Ghost and composed enhancement delivery

Demonstrate visually distinct projection and every enhanced lifecycle interaction in a built playable game.

Exit: demonstrate this integrated capability, review its code and relevant dependencies, run focused acceptance/regressions, repair blockers and retain a milestone report/HANDOFF. TASKS assigns these obligations to the appropriate final boundary task under the review-unit policy. Feedback may support a human decision to continue, amend, simplify or stop; it does not automatically change authorized scope.

### Milestone 2.4 — Phase review

Exactly one phase code-review/testing/report outcome after every delivery milestone is verified and closed. Verify cross-milestone behavior, the phase exits below and carried findings; repair blockers, retain the phase report and aggregate deferred TODOs. When this is the final phase of the complete intended task list, also retain the final implementation report/TODO aggregation. This special review milestone is not a delivery-count target.

Phase exits: Demonstrate hold/replacement, wall kicks and ghost/drop agreement under 1000 ms grounding delay, including failed moves, grounded transformations and hold boundaries. Re-run prior useful gameplay in both browsers, update guides/build/version and review the composed lifecycle.

Integration/release boundary: complete all phase tasks/reports and applicable hosted closures, explicitly integrate into the recorded target, verify the merged build and relevant regressions, publish/read back the default-branch release commit/tag, then publish release notes for v0.2.0. A partial phase stops on its working branch. No later capability is required for this phase’s scoped exit.

## Phase 3 — Conditional ghost visibility

Outcome and included scope: Dynamic ghost rendering only; hide upper-half and straddling projections while preserving landing/drop geometry and enhanced gameplay.

Dependency: Phase 2 verified, integrated and published.

Contracts: V01, E02, Q01. Target release: v0.3.0.

### Milestone 3.1 — Dynamic projection visibility

A player can see the ghost disappear/reappear around the midline without movement or timing changes.

Exit: demonstrate this integrated capability, review its code and relevant dependencies, run focused acceptance/regressions, repair blockers and retain a milestone report/HANDOFF. TASKS assigns these obligations to the appropriate final boundary task under the review-unit policy. Feedback may support a human decision to continue, amend, simplify or stop; it does not automatically change authorized scope.

### Milestone 3.2 — Phase review

Exactly one phase code-review/testing/report outcome after every delivery milestone is verified and closed. Verify cross-milestone behavior, the phase exits below and carried findings; repair blockers, retain the phase report and aggregate deferred TODOs. When this is the final phase of the complete intended task list, also retain the final implementation report/TODO aggregation. This special review milestone is not a delivery-count target.

Phase exits: Demonstrate visibility at min projected row 9 versus 10 and for straddling/rotated pieces in both browsers; hard drop still lands identically when the ghost is hidden. Update guidance and v0.3.0 package.

Integration/release boundary: complete all phase tasks/reports and applicable hosted closures, explicitly integrate into the recorded target, verify the merged build and relevant regressions, publish/read back the default-branch release commit/tag, then publish release notes for v0.3.0. A partial phase stops on its working branch. No later capability is required for this phase’s scoped exit.
