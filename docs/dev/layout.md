# Repository layout

## Status and ownership

The root guidance/policy files, bundled agent packages and docs/dev preparation records already exist. Paths below allocate intended application code and checks; their presence and implementation are not claimed. [DECOMPOSITION](DECOMPOSITION.md) owns logical boundaries and [PLAN](PLAN.md) delivery. Keep production code independent of test fixtures and browser installation paths.

| Owner | Intended source / configuration | Intended checks |
| --- | --- | --- |
| C01 Geometry | src/core/geometry.ts | tests/unit/geometry.test.ts; tests/fixtures/shapes |
| C02 Board | src/core/board.ts | tests/unit/board.test.ts; tests/fixtures/boards |
| C03 PieceSource | src/core/source.ts | tests/unit/source.test.ts |
| C04 Game | src/core/game.ts; src/core/types.ts for shared plain-data contracts | tests/unit/game.test.ts; tests/integration/lifecycle.test.ts |
| C05 Clock | src/browser/clock.ts | tests/unit/clock.test.ts; tests/integration/runtime.test.ts |
| C06 Input | src/browser/input.ts | tests/unit/input.test.ts; tests/e2e/keyboard.spec.ts |
| C07 View | src/browser/view.ts; src/styles.css | tests/e2e/rendering.spec.ts and focused snapshot/view checks |
| C08 Runtime | src/browser/runtime.ts; src/main.ts composition entry | tests/integration/runtime.test.ts; tests/e2e/lifecycle.spec.ts |
| Static build | index.html; package.json and lockfile; tsconfig.json; vite.config.ts | typecheck/build scripts and built-app smoke coverage |
| Test harness | vitest.config.ts; playwright.config.ts; tests/support | Unit/integration commands and actual static-server browser suite |
| C09 Landing and rotation fixtures | src/core/landing.ts; geometry.ts remains canonical shape/kick owner | tests/unit/landing.test.ts; tests/fixtures/rotation; tests/e2e/enhancements.spec.ts |
| Dynamic ghost visibility | src/browser/view.ts; a pure exported predicate may be colocated there | tests/unit/ghost-visibility.test.ts; tests/e2e/ghost.spec.ts |
| Penetrator policy/inventory/appearance | landing.ts and game.ts own rules; board.ts retains settled appearance; view.ts owns rendering | tests/fixtures/penetration; tests/unit/penetration.test.ts; tests/e2e/penetrator.spec.ts |

## Dependency and placement rules

Core imports only core/plain types; it must not import browser modules, document/window, runner packages or fixture files. Browser adapters import core and compose through Runtime. Geometry owns canonical shapes/rotation data; board owns settled mutation; Game orchestrates transitions without copying geometry or rendering rules. Put shared public snapshot/command types with core, not in a browser utility bucket. Colocate narrowly scoped pure helpers with their owner unless an independently meaningful module is justified.

## Documentation and generated files

README.md owns truthful setup/play/check navigation. docs/user/CONTROLS.md and CONFIGURATION.md where applicable own concise player guidance; docs/dev roots own design, contracts, delivery and task evidence. Required adjacent SPEC/PLAN/TASKS review reports remain in docs/dev. Implementation reports use docs/dev/reports/phases/<phase>/<milestone>.md and PHASE-REPORT.md; final aggregation is docs/dev/reports/IMPLEMENTATION-REPORT.md. RELEASE-NOTES.md at root owns the current prepared release message. Retain bundled skills, policies, provenance scaffolding and closed records unchanged outside their separately authorized scope.

dist/, node_modules/, test-results/, playwright-report/, owned browser binaries/caches and disposable screenshots/profiles are generated outputs, excluded from tracked production assets. Configure an absolute dedicated browser path outside tracked source for both install and execution; do not use personal/system installations. Keep reproducible fixtures in tests/fixtures and temporary evidence in owned generated locations. Hosting credentials remain ignored conventional root inputs and never enter builds, screenshots or reports.

## Planned commands

T-001 will establish and validate npm scripts for typecheck, unit/integration tests, static build and Playwright tests against the actual application. These are intended responsibilities, not currently working commands. Document the exact commands and pinned versions after execution; keep browser installation distinct from application acceptance.
