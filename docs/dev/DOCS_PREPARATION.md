# Main documentation preparation record

## Current control

- Mode: autodoc/autoloop, explicitly requested in the project prompt of 2026-10-24.
- Delivery mode: strict multipass. Preserve established phase/task IDs, names, scope, parentage, order, dependencies and exits; add later scope in subsequent bounded ranges. No flexible exception is granted.
- Current pass: 4. Cursor: DOCS-007 accepted/preapproved; finish publication and hosted closure before advancing.
- Approval basis: first PROJECT and recorded cross-scope proposals approved by the user’s “Approve” reply on 2026-10-24, accepting published proposal e5fa48fd34e3f38bd99d3872c861313362478add. Later PROJECT approvals are waived under the announced autoloop selection; subsequent document checkpoints through TASKS are preapproved. Initial approval authorizes the agreed six-pass sequence and resets. New material autoloop decisions are delegated after that approval, with recorded rationale and visible updates.
- Tracking: enabled for preparation and implementation by existing root AGENTS.md. Milestone `sdd-docs-main` #1 and DOCS-001–009 issues #1–9 were created and read back with exact standard content and associations before the first repository modification.
- Publication: push/read back every owned commit before further work. Actual default/integration target is `main`.
- Boundary: initial approval received; run the six predefined passes through final DOCS-008, then stop before DOCS-009. Implementation is not yet authorized.
- Reporting: Explicit bootstrap, then Standard; Minimal and Explicit remain available.

## Scope sequence

1. **Playable classic baseline.** Falling tetrominoes, movement, rotation, gravity, line clearing, scoring, game over and restart. Keep this coherent and minimal; later features are excluded from the initial product documents.
2. **Gameplay enhancements.** Hold, ghost, 7-bag randomization, wall kicks and hard drop. Default lock delay is one full gravity interval from grounding, including after hard drop.
3. **Conditional ghost visibility.** Hide a ghost whose landing projection is above the midline; restore visibility in the lower half. Apply the proposed straddling rule below if accepted.
4. **Penetrator mode.** Hotkey activation spends one bonus; pass through occupied cells without destroying them until lock. Final placement is entirely inside the board and does not overlap. Hard drop and ghost share the lowest valid landing. A four-line clear earns one bonus, capped at three. Penetrators are entirely white; regular pieces are not white. Display one symbol per bonus and refresh on earning/spending.
5. **Session-only configuration.** Side-panel ghost mode (hide/dynamic/show), hard drop on/off, next preview on/off, hard-drop locking (general/immediate), general locking (failed downward attempt/full interval), hold on/off. Add next preview here. Settings survive restart within the page but reset on reload; no persistence in this scope.
6. **Configuration persistence.** Resolve each setting independently from valid explicit URL parameter, valid cookie, then default. Save valid explicit URL values to cookies even at defaults. Omitted parameters retain saved values. Every control change saves its cookie and updates its query parameter. Invalid inputs and unavailable storage follow the proposals below if accepted.

## Per-pass decisions

All entries below originate in initial exploration, pass 1. The user approved the published brief and these cross-scope proposals on 2026-10-24. Their original agent-proposal provenance is retained; status is now accepted. Future-applicable choices remain here until their corresponding scope is adopted.

| Pass / decision | Resolution and rationale | Basis / source | Applicability / status |
| --- | --- | --- | --- |
| 1 / Product boundary | Single-player desktop-browser game; keyboard interaction; static delivery without backend, account, leaderboard, touch controls or audio. These keep the requested baseline small. | User browser-game scope; proposed exclusions | All scopes; accepted |
| 1 / Delivery technology | TypeScript, Canvas board and ordinary DOM status/controls, with a small static build. Plain JavaScript reduces tooling but gives fewer state checks; a component framework adds machinery unnecessary for this control panel. | Agent recommendation for human approval; package/tool versions deferred | All scopes; accepted |
| 1 / Baseline mechanics | 10 columns by 20 visible rows, fixed one-second gravity, independently uniform tetromino selection, clockwise rotation rejected on collision, immediate locking after failed descent, and line-clear scoring 100/300/500/800. No leveling or speed progression is requested. | Minimal baseline interpretation; exact mechanics to be specified after approval | Scope 1; accepted |
| 1 / Enhancement semantics | SRS wall kicks; one hold per active piece, replenished after lock; replacement spawns at its initial orientation. Hold and restart do not carry a partially elapsed lock timer into the new piece. | Agent proposal preserving predictable input | Scopes 2–6; accepted |
| 1 / Midline | Show the dynamic ghost only when every projected cell is in the lower half. A straddling projection is hidden; for a 20-row board the lower half is rows 10–19 with zero-based indices. | Conservative whole-piece interpretation of upper/lower half | Scopes 3–6; accepted |
| 1 / Lock timing | Start one full interval when grounding begins. Grounded moves/rotations and repeated hard drops do not extend it. Leaving support cancels the grounded timer; a later touchdown starts a full interval. Freeze gameplay time while suspended/hidden; no catch-up on return. Hard drop to an already grounded position retains elapsed time. | Agent proposal to avoid unlimited grounded resets and background surprises | Scopes 2–6; accepted |
| 1 / Penetrator hold and lifecycle | Disable hold while penetrator is active. Activation spends exactly one bonus, cannot be toggled off/refunded and ends on lock or game over. Holding an ordinary piece retains ordinary hold rules; no stored penetrator state exists. Restart clears bonuses. | Agent proposal preventing ability storage/exchange exploits; awaiting this project's acceptance | Scopes 4–6; accepted |
| 1 / Penetrator landing safety | Traverse occupied rows without changing settled cells. Use one lowest-valid-landing calculation for gravity, hard drop and ghost. Never merge an overlapping transient position. Reject activation/movement/rotation if it leaves no in-bounds non-overlapping landing at or below the candidate position; do not spend a bonus for rejected activation. Activation is not a timer-reset action; recalculate grounding if its landing changes. | Agent proposal resolving overlap/locking and stranded-piece ambiguity | Scopes 4–6; accepted |
| 1 / Midgame settings | Visibility, preview and action availability change immediately. Turning hold off retains the held slot; re-enabling does not reset hold eligibility. Snapshot the two locking policies for each new active piece; changes apply on next spawn, including hold replacement. Configuration does not reset the board, score, bonuses or timers. | Agent proposal avoiding retroactive timing changes | Scopes 5–6; accepted |
| 1 / Defaults | Ghost dynamic, hard drop on, preview on, hard-drop locking follows general, general full-interval, hold on. The new configurable defaults preserve the previously delivered behavior. | Agent proposal; preview first appears in scope 5 | Scopes 5–6; accepted |
| 1 / Invalid settings | Validate each source independently. Invalid URL value falls through to valid cookie/default without overwriting the cookie. Invalid cookie falls through to default. Duplicate instances of the same setting parameter are invalid rather than guessed. Preserve unrelated query parameters and fragments; URL changes use history replacement. | Agent proposal for deterministic, non-destructive resolution | Scope 6; accepted |
| 1 / Persistence resilience | Use per-setting cookies with a one-year lifetime, Path=/ and SameSite=Lax; Secure on HTTPS. Persist valid explicit URL values, including defaults. If cookies or URL updates are unavailable, keep the game/settings usable in memory and retain whichever persistence channel works. Cookie scope assumes one game instance per origin path policy; no game-state persistence is requested. | Agent proposal; deployment details can be refined before implementation | Scope 6; accepted |
| 1 / Browsers and verification | Follow BROWSER_DEV_POLICY.md: isolated Chromium primary and managed Firefox secondary, headless interaction/rendering sufficient. No browser installation is needed for documentation. Later tasks must provision and prove actual harness capability before dependent acceptance; do not silently remove a required browser. | Existing repository policy; proposed Playwright harness | All scopes; policy and harness accepted |
| 1 / Versions and releases | First verified classic release v0.1.0; later additive pre-1.0 delivery phases increment minor versions, repairs patch versions. Plan the exact version/phase mapping when scope arrives. Publish release/tag/notes after each authorized, verified and integrated implementation phase. No documentation-only release or initial preparation tag. | Explicit user release instruction; agent version recommendation | Future implementation; accepted mapping, release obligation active |

## Cross-scope decisions

| Concern | Decision / applicable scopes | Reconsideration condition |
| --- | --- | --- |
| Ghost geometry | Midline and penetrator-landing proposals above govern scopes 3–6; visibility never changes the landing calculation. | Board geometry or requested visibility interpretation changes |
| Timing and configuration | Lock timing and per-piece policy snapshots above govern scopes 2–6. Availability controls cannot reset a timer or restore a consumed hold. | Explicit user steering or a discovered conflicting contract |
| Penetration and hold | Penetrator lifecycle/landing safety above govern scopes 4–6; invalid positions are transient only. | A requested change to activation or traversal rules |
| Durable settings | Defaults, independent validation and persistence resilience above govern scopes 5–6; scope 5 intentionally has no reload persistence. | URL schema, deployment scope or storage requirement changes |
| Delivery preservation | Strict multipass protects each established PLAN/TASKS range; later scope gets new bounded phases/tasks. | Explicit scoped permission to alter protected delivery ranges |

## Decisions and document evidence

| Task | Current evidence / decision basis |
| --- | --- |
| DOCS-001 | Initialization e8cf495287969eaf7d3c5e0f400eef066fe0cc9a published/readback verified; four existing root files preserved; issue #1 closed/readback verified. |
| DOCS-002 | Scope 4: local accepted/preapproved completion; `PROJECT.md` SHA-256 `63ccd6d83f063437c7cb08aef495b61fc151e7d96c9bab59f0452304315e2ed8`; see qualified acceptance/QC evidence below. Publication/issue effects are established by their actual readbacks. |
| DOCS-003 | Scope 4: local accepted/preapproved completion; `ARCHITECTURE.md` SHA-256 `87c9a8db3f2f3c6a259e5a1dbcb602ad13b348ff3b096541693f0e1112fea2fa`; see qualified acceptance/QC evidence below. Publication/issue effects are established by their actual readbacks. |
| DOCS-004 | Scope 4: local accepted/preapproved completion; `DECOMPOSITION.md` SHA-256 `4b4051032c5f3442ee6f10d91afde8bc1c1124f33ba8d4e60209eeb9664a6d02`; see qualified acceptance/QC evidence below. Publication/issue effects are established by their actual readbacks. |
| DOCS-005 | Scope 4: local accepted/preapproved completion; `SPEC.md` SHA-256 `cc026f6700e6b28470cb208a9696dc9109f3a36ddb684a57003c0c7f6f2a370f`; see qualified acceptance/QC evidence below. Publication/issue effects are established by their actual readbacks. |
| DOCS-006 | Scope 4: local accepted/preapproved completion; `PLAN.md` SHA-256 `eef1777c5bbb4ab5cbaf01a459095ba48a5d3950b2d711e87feda7695f185ca6`; see qualified acceptance/QC evidence below. Publication/issue effects are established by their actual readbacks. |
| DOCS-007 | Scope 4: local accepted/preapproved completion; `layout.md` SHA-256 `bfc6feca6b587dbb14efe634fe937d78d498c9dbc260653fcca59ba8a794ab1f`; see qualified acceptance/QC evidence below. Publication/issue effects are established by their actual readbacks. |
| DOCS-008 | Scope 4: not complete in this scope; retained document is a prior-scope input until revised and rechecked. |
| DOCS-009 | Not selected; unchecked/open. Whole-package QC and integration remain outside the autoloop boundary. |

## Initialization and current reset

- Original root presence: all four existed — AI_DISCLOSURE.md, SDD-MANAGER.md, AGENTS.md and SKILL_DISCOVERY_PROTOCOL.md. Retained all four; copied none. Compared bytes with initial Git blobs; preservation passed. All-present initialization adds no continuation pause.
- Package: bundled SDD Manager 0.15.2 at initial commit. Coordinator and initialization/tracking assets match the installed running package after newline normalization; copies use repository package bytes.
- Manual provenance: default enabled. Seed 44373f66c78be757a9455effcf61ad85743c1945 on design-docs/ai-logs from main at 893cffb7da0ac90abadb469c7e117a085e8286f3; explicit two-parent merge 62169f0ad3764882e22400b4881903758c88d94b on main. Both pushes/readbacks matched with confirmed cleanup. Both scaffold files byte-match package assets. No transcript created.
- Branch: design-docs/main created from main at 62169f0ad3764882e22400b4881903758c88d94b; target main. Existing branch and root instructions retained.
- Credentials: repository-local conventional credential is excluded by *.tkn and untracked; no secret belongs in tracked records.
- Current reset: scope 3 complete at b2a15c7347d942d5c5e30b0a72a6cfdc8863d594; advance to predefined scope 4 under user-approved autoloop.

## Pending transitions

Publish/read back the current completion commit and close/read back issue #7. Then continue in dependency order within the six-pass sequence. Final stop: pass 6 DOCS-008, before DOCS-009, package integration or implementation.

## Active-pass document evidence

- Pass 1, DOCS-002: `PROJECT.md` SHA-256 `33acd8f5dc87a14c08d80ec3d2594cd4dff3df7ce61b3d72613216d1a6ffbf23`. Human acceptance of exact proposal e5fa48fd34e3f38bd99d3872c861313362478add on 2026-10-24; unchanged brief bytes retained. Scope and boundary review passed; later document approvals are covered by autodoc/autoloop. Publication and issue #2 closure require readback after the containing commit.
- Pass 1, DOCS-003: `ARCHITECTURE.md` SHA-256 `f9996c379aa8ccaab7a6c3a27470407a521bf7635f0a658c46d2cbdf31704561`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Ownership, dependency direction, time/random injection and browser/core separation reviewed; no cycles or duplicate state owners required. Publication and issue #3 closure require readback after the containing commit.

- Pass 1, DOCS-004: `DECOMPOSITION.md` SHA-256 `7adb4ecc97001d962cd3a4e6a295a43ba9aeec74ab1b747bd498a3931cca4e3b`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Component interfaces, state/resource ownership, rejection/failure and verification seams reviewed against architecture. Publication and issue #4 closure require readback after the containing commit.

- Pass 1, DOCS-005: `SPEC.md` SHA-256 `a2af25d0a97850759fa172fabc11907ab9bce9d23ffd208cff6785e4fc09dd4d`; `SPEC-REVIEW-REPORT.md` SHA-256 `723c5dc6509650e8de6de2d6d706a5e0ec657c4cc2cd4f51878bc8e5959ef23f`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Current review: SPEC-REVIEW-REPORT.md.  Publication and issue #5 closure require readback after the containing commit.

- Pass 1, DOCS-006: `PLAN.md` SHA-256 `5cff4b2cbc26db87ba89e7d3cc180b2af261fbc4a6afeb1cc9a9636890bc9e9c`; `PLAN-REVIEW-REPORT.md` SHA-256 `9d8e7f1c74610d566f41f680fdc9f04363bc2c4a578002d7e3b7df51c101c96a`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Protected earlier PLAN/TASKS text compared and preserved; current counts and concrete scope reviewed. Current review: PLAN-REVIEW-REPORT.md.  Publication and issue #6 closure require readback after the containing commit.

- Pass 1, DOCS-007: `layout.md` SHA-256 `733816e7f4350020f465a247befaa63588d90430ad9bb88cc7abfa66599228ff`; `PLAN-REVIEW-REPORT.md` SHA-256 `e3f4689edc0345880b7b046d4a33150416726b83ee66997940c922bac2e54f7a`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Current review: PLAN-REVIEW-REPORT.md.  Publication and issue #7 closure require readback after the containing commit.

- Pass 1, DOCS-008: `TASKS.md` SHA-256 `37de6ae4bdfb041916252d19c71fb6fb645b1f0243a13d31fc61b2ebaa3ff906`; `TASKS-REVIEW-REPORT.md` SHA-256 `172e3cd17513a813515f04ad923ba0e6c99c553c240d032150ec60fa9ed7ee9b`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Protected earlier PLAN/TASKS text compared and preserved; current counts and concrete scope reviewed. Current review: TASKS-REVIEW-REPORT.md.  Publication and issue #8 closure require readback after the containing commit.

- Pass 2, DOCS-002: `PROJECT.md` SHA-256 `db4b3a1288744382f98fe1004be5cf4df0f0f82bdeb9ff50565213642a79938a`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed.  Publication and issue #2 closure require readback after the containing commit.

- Pass 2, DOCS-003: `ARCHITECTURE.md` SHA-256 `811cd6c653a964e8673e68689759f6fd888b853942a8ed947316ff3a17267c39`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Ownership, dependency direction, time/random injection and browser/core separation reviewed; no cycles or duplicate state owners required. Publication and issue #3 closure require readback after the containing commit.

- Pass 2, DOCS-004: `DECOMPOSITION.md` SHA-256 `b62510b57ec26cbad651a02cf2f2210f78c45367c9ed0da5a0679a425aa5f525`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Component interfaces, state/resource ownership, rejection/failure and verification seams reviewed against architecture. Publication and issue #4 closure require readback after the containing commit.

- Pass 2, DOCS-005: `SPEC.md` SHA-256 `e225fdd48af55311e406e1d9c85ac0dd6f21acfe8c73477d215d2917124b7d95`; `spec/ROTATION.md` SHA-256 `d0deb5c15e14bf490a1ee492364eb1b860b131b9fce470315bf9103c4b7aaff5`; `SPEC-REVIEW-REPORT.md` SHA-256 `dc860b7333ec3c4132e850826df48e3e50f5b95332e54d253777ec46d84535a8`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Current review: SPEC-REVIEW-REPORT.md.  Publication and issue #5 closure require readback after the containing commit.

- Pass 2, DOCS-006: `PLAN.md` SHA-256 `01be71da4b8d0ed0055564e9823bde9b46e5d7078ac9876c034cfd9f62298012`; `PLAN-REVIEW-REPORT.md` SHA-256 `d7b2c01ca328b2f7353a5e298c0ff291f7905b966b5ba8ea37f4cd89dcef41a2`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Protected earlier PLAN/TASKS text compared and preserved; current counts and concrete scope reviewed. Current review: PLAN-REVIEW-REPORT.md.  Publication and issue #6 closure require readback after the containing commit.

- Pass 2, DOCS-007: `layout.md` SHA-256 `51b307adef4cf25898475c402011ab7e8e369b838fc6780f3edc10bdf3b4e4f6`; `PLAN-REVIEW-REPORT.md` SHA-256 `c4b2bf493a03282d65a1fc6836ceb29c9ad1328d7a44b64818fc1091fda4f225`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Current review: PLAN-REVIEW-REPORT.md.  Publication and issue #7 closure require readback after the containing commit.

- Pass 2, DOCS-008: `TASKS.md` SHA-256 `23bd860592d87719a47ab37e90e06195f95134c21093ad97cef2ac35e11cf1b3`; `TASKS-REVIEW-REPORT.md` SHA-256 `70bb6c3a8bd16d47a67afb67da07a1b9ec7025ef4c41d7678026baece78e6e44`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Protected earlier PLAN/TASKS text compared and preserved; current counts and concrete scope reviewed. Current review: TASKS-REVIEW-REPORT.md.  Publication and issue #8 closure require readback after the containing commit.

- Pass 3, DOCS-002: `PROJECT.md` SHA-256 `740d44096d52faa8cbefb206fa07775f607050f5204c3cdb346b23138175cbee`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed.  Publication and issue #2 closure require readback after the containing commit.

- Pass 3, DOCS-003: `ARCHITECTURE.md` SHA-256 `809c956e8633d6bf64c6b03f05371c9f33c4160462455b18f559e4916feeaddc`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Ownership, dependency direction, time/random injection and browser/core separation reviewed; no cycles or duplicate state owners required. Publication and issue #3 closure require readback after the containing commit.

- Pass 3, DOCS-004: `DECOMPOSITION.md` SHA-256 `0bcabd6552da1d6c63a8c618fbe77c39875d6f4df9cd94fd6ac1e04c37b2456e`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Component interfaces, state/resource ownership, rejection/failure and verification seams reviewed against architecture. Publication and issue #4 closure require readback after the containing commit.

- Pass 3, DOCS-005: `SPEC.md` SHA-256 `7f30ab4dff677d212d77f141ae47e26b6bdebc747817807cfc3926b4ffb443b3`; `spec/ROTATION.md` SHA-256 `d0deb5c15e14bf490a1ee492364eb1b860b131b9fce470315bf9103c4b7aaff5`; `SPEC-REVIEW-REPORT.md` SHA-256 `bda9d5f7ec49f4eef9d76905884964646fd6eda624f8a6c092a1c2bbfc8ea685`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Current review: SPEC-REVIEW-REPORT.md.  Publication and issue #5 closure require readback after the containing commit.

- Pass 3, DOCS-006: `PLAN.md` SHA-256 `44be4b64bb7b7133faf52ebb0641eb51398ba01f8124cc8627836111010e9298`; `PLAN-REVIEW-REPORT.md` SHA-256 `870ee41c13ba7b36ad3583391599bb32b222050496cd2254ee28b1ddd6886f7e`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Protected earlier PLAN/TASKS text compared and preserved; current counts and concrete scope reviewed. Current review: PLAN-REVIEW-REPORT.md.  Publication and issue #6 closure require readback after the containing commit.

- Pass 3, DOCS-007: `layout.md` SHA-256 `63387301c084dd33f23183de1c031c7bbe481954358b0236301a5a2d86748aef`; `PLAN-REVIEW-REPORT.md` SHA-256 `9c23bc9d37272ae53a1280a1715fc13452fd98bcda14885e43b4d515f084696c`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Current review: PLAN-REVIEW-REPORT.md.  Publication and issue #7 closure require readback after the containing commit.

- Pass 3, DOCS-008: `TASKS.md` SHA-256 `f8953d44f735c393ef5e8e491af341b8e77fa83689121e90d5a7d65b8a791d7d`; `TASKS-REVIEW-REPORT.md` SHA-256 `15d29370f714001a097e13372f552f849f2a7a0fa1c4b63bf11802debedaad28`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Protected earlier PLAN/TASKS text compared and preserved; current counts and concrete scope reviewed. Current review: TASKS-REVIEW-REPORT.md.  Publication and issue #8 closure require readback after the containing commit.

- Pass 4, DOCS-002: `PROJECT.md` SHA-256 `63ccd6d83f063437c7cb08aef495b61fc151e7d96c9bab59f0452304315e2ed8`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed.  Publication and issue #2 closure require readback after the containing commit.

- Pass 4, DOCS-003: `ARCHITECTURE.md` SHA-256 `87c9a8db3f2f3c6a259e5a1dbcb602ad13b348ff3b096541693f0e1112fea2fa`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Ownership, dependency direction, time/random injection and browser/core separation reviewed; no cycles or duplicate state owners required. Publication and issue #3 closure require readback after the containing commit.

- Pass 4, DOCS-004: `DECOMPOSITION.md` SHA-256 `4b4051032c5f3442ee6f10d91afde8bc1c1124f33ba8d4e60209eeb9664a6d02`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Component interfaces, state/resource ownership, rejection/failure and verification seams reviewed against architecture. Publication and issue #4 closure require readback after the containing commit.

- Pass 4, DOCS-005: `SPEC.md` SHA-256 `cc026f6700e6b28470cb208a9696dc9109f3a36ddb684a57003c0c7f6f2a370f`; `spec/ROTATION.md` SHA-256 `d0deb5c15e14bf490a1ee492364eb1b860b131b9fce470315bf9103c4b7aaff5`; `SPEC-REVIEW-REPORT.md` SHA-256 `39c0fcce7fc2c44e1ea3e85982f6fb6014677ceddc357d722c6334694401e235`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Current review: SPEC-REVIEW-REPORT.md.  Publication and issue #5 closure require readback after the containing commit.

- Pass 4, DOCS-006: `PLAN.md` SHA-256 `eef1777c5bbb4ab5cbaf01a459095ba48a5d3950b2d711e87feda7695f185ca6`; `PLAN-REVIEW-REPORT.md` SHA-256 `8caeca804dd9b7026e58a335f094b886c0118dcc9187c9d167dcf0ab737f6f8f`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Protected earlier PLAN/TASKS text compared and preserved; current counts and concrete scope reviewed. Current review: PLAN-REVIEW-REPORT.md.  Publication and issue #6 closure require readback after the containing commit.

- Pass 4, DOCS-007: `layout.md` SHA-256 `bfc6feca6b587dbb14efe634fe937d78d498c9dbc260653fcca59ba8a794ab1f`; `PLAN-REVIEW-REPORT.md` SHA-256 `67c47170df9b8071fe063b1687945fade4a6989abd30d829681c99a0a970762e`. Scoped autodoc/autoloop preapproval from the user-approved initial sequence; current-scope conformance/content review passed. Current review: PLAN-REVIEW-REPORT.md.  Publication and issue #7 closure require readback after the containing commit.

## Scope 1 completion and protected range

Scope: Playable classic baseline. Current owned phase: 1; task range T-001–T-010. PLAN SHA-256 `5cff4b2cbc26db87ba89e7d3cc180b2af261fbc4a6afeb1cc9a9636890bc9e9c`; TASKS SHA-256 `37de6ae4bdfb041916252d19c71fb6fb645b1f0243a13d31fc61b2ebaa3ff906`. Earlier ranges retained exactly; current document QC is scoped and package QC remains unselected. The containing DOCS-008 completion commit is the retained source checkpoint for the next reset.

## Reset to scope 2

Retained prior checkpoint fc44b43673abfa90b7d9c432ca4969951595bcb1, all product documents and scopes 1–1 phase/task ranges. Reason: predefined cumulative addition — Gameplay enhancements. DOCS-002–009 reset together, DOCS-001 retained complete. User initial approval authorizes this reset and later PROJECT preapproval. Publish/read back, then reopen/read back existing issues #2–9; no document work until complete.

## Scope 2 decision summary

Carried the accepted hold/grounding decisions forward. Delegated detail: clockwise-only SRS uses explicit screen-y-down tables; C is hold and Space hard drop. Seven-bag uses Fisher–Yates and read-only peek. Phase 2 adds the full enhancement lifecycle without changing phase 1. Basis: user-approved initial scope sequence and autoloop delegation; initial human decisions remain accepted, these additional details are agent-owned. Applicability: this and later scopes; active unless changed by user steering or a discovered conflict.

## Scope 2 completion and protected range

Scope: Gameplay enhancements. Current owned phase: 2; task range T-011–T-020. PLAN SHA-256 `01be71da4b8d0ed0055564e9823bde9b46e5d7078ac9876c034cfd9f62298012`; TASKS SHA-256 `23bd860592d87719a47ab37e90e06195f95134c21093ad97cef2ac35e11cf1b3`. Earlier ranges retained exactly; current document QC is scoped and package QC remains unselected. The containing DOCS-008 completion commit is the retained source checkpoint for the next reset.

## Reset to scope 3

Retained prior checkpoint 2488208a4b5f0236795866a474aa4412f90f536e, all product documents and scopes 1–2 phase/task ranges. Reason: predefined cumulative addition — Conditional ghost visibility. DOCS-002–009 reset together, DOCS-001 retained complete. User initial approval authorizes this reset and later PROJECT preapproval. Publish/read back, then reopen/read back existing issues #2–9; no document work until complete.

## Scope 3 decision summary

No new material choice: carried the human-approved whole-projection min-y rule forward. A straddling projection is hidden; visibility is independent of landing/drop. Phase 3 is intentionally one narrow delivery milestone. Basis: user-approved initial scope sequence and autoloop delegation; initial human decisions remain accepted, these additional details are agent-owned. Applicability: this and later scopes; active unless changed by user steering or a discovered conflict.

## Scope 3 completion and protected range

Scope: Conditional ghost visibility. Current owned phase: 3; task range T-021–T-023. PLAN SHA-256 `44be4b64bb7b7133faf52ebb0641eb51398ba01f8124cc8627836111010e9298`; TASKS SHA-256 `f8953d44f735c393ef5e8e491af341b8e77fa83689121e90d5a7d65b8a791d7d`. Earlier ranges retained exactly; current document QC is scoped and package QC remains unselected. The containing DOCS-008 completion commit is the retained source checkpoint for the next reset.

## Reset to scope 4

Retained prior checkpoint b2a15c7347d942d5c5e30b0a72a6cfdc8863d594, all product documents and scopes 1–3 phase/task ranges. Reason: predefined cumulative addition — Penetrator mode. DOCS-002–009 reset together, DOCS-001 retained complete. User initial approval authorizes this reset and later PROJECT preapproval. Publish/read back, then reopen/read back existing issues #2–9; no document work until complete.

## Scope 4 decision summary

Carried approved penetration/hold/landing safeguards forward. Delegated detail: B activates; valid landing is the deepest non-overlapping anchor at/below current y. Transit may overlap, but candidate transforms must preserve a future landing and every merge rejects overlap. Settled penetrator appearance remains white without active ability. Basis: user-approved initial scope sequence and autoloop delegation; initial human decisions remain accepted, these additional details are agent-owned. Applicability: this and later scopes; active unless changed by user steering or a discovered conflict.
