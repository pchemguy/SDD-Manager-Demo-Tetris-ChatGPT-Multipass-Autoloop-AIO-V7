# Main documentation preparation record

## Current control

- Mode: autodoc/autoloop, explicitly requested in the project prompt of 2026-10-24.
- Delivery mode: strict multipass. Preserve established phase/task IDs, names, scope, parentage, order, dependencies and exits; add later scope in subsequent bounded ranges. No flexible exception is granted.
- Current pass: 1, playable classic baseline. Cursor: DOCS-002 proposal preparation after verified initialization publication and issue closure.
- Approval basis: first PROJECT human approval is pending. Later PROJECT approvals are waived under the announced autoloop selection; subsequent document checkpoints through TASKS are preapproved. Initial approval will authorize the agreed six-pass sequence and resets. New material autoloop decisions are delegated after that approval, with recorded rationale and visible updates.
- Tracking: enabled for preparation and implementation by existing root AGENTS.md. Milestone `sdd-docs-main` #1 and DOCS-001–009 issues #1–9 were created and read back with exact standard content and associations before the first repository modification.
- Publication: push/read back every owned commit before further work. Actual default/integration target is `main`.
- Boundary: present the first PROJECT for approval before ARCHITECTURE. After approval run the six predefined passes through final DOCS-008, then stop before DOCS-009. Implementation is not yet authorized.
- Reporting: Explicit bootstrap, then Standard; Minimal and Explicit remain available.

## Scope sequence

1. **Playable classic baseline.** Falling tetrominoes, movement, rotation, gravity, line clearing, scoring, game over and restart. Keep this coherent and minimal; later features are excluded from the initial product documents.
2. **Gameplay enhancements.** Hold, ghost, 7-bag randomization, wall kicks and hard drop. Default lock delay is one full gravity interval from grounding, including after hard drop.
3. **Conditional ghost visibility.** Hide a ghost whose landing projection is above the midline; restore visibility in the lower half. Apply the proposed straddling rule below if accepted.
4. **Penetrator mode.** Hotkey activation spends one bonus; pass through occupied cells without destroying them until lock. Final placement is entirely inside the board and does not overlap. Hard drop and ghost share the lowest valid landing. A four-line clear earns one bonus, capped at three. Penetrators are entirely white; regular pieces are not white. Display one symbol per bonus and refresh on earning/spending.
5. **Session-only configuration.** Side-panel ghost mode (hide/dynamic/show), hard drop on/off, next preview on/off, hard-drop locking (general/immediate), general locking (failed downward attempt/full interval), hold on/off. Add next preview here. Settings survive restart within the page but reset on reload; no persistence in this scope.
6. **Configuration persistence.** Resolve each setting independently from valid explicit URL parameter, valid cookie, then default. Save valid explicit URL values to cookies even at defaults. Omitted parameters retain saved values. Every control change saves its cookie and updates its query parameter. Invalid inputs and unavailable storage follow the proposals below if accepted.

## Per-pass decisions

All entries below originate in initial exploration, pass 1. They are agent proposals for the first approval, not accepted user instructions. Future-applicable decisions remain here until the corresponding scope is adopted. No later document set has been drafted.

| Pass / decision | Resolution and rationale | Basis / source | Applicability / status |
| --- | --- | --- | --- |
| 1 / Product boundary | Single-player desktop-browser game; keyboard interaction; static delivery without backend, account, leaderboard, touch controls or audio. These keep the requested baseline small. | User browser-game scope; proposed exclusions | All scopes; proposed |
| 1 / Delivery technology | TypeScript, Canvas board and ordinary DOM status/controls, with a small static build. Plain JavaScript reduces tooling but gives fewer state checks; a component framework adds machinery unnecessary for this control panel. | Agent recommendation for human approval; package/tool versions deferred | All scopes; proposed |
| 1 / Baseline mechanics | 10 columns by 20 visible rows, fixed one-second gravity, independently uniform tetromino selection, clockwise rotation rejected on collision, immediate locking after failed descent, and line-clear scoring 100/300/500/800. No leveling or speed progression is requested. | Minimal baseline interpretation; exact mechanics to be specified after approval | Scope 1; proposed |
| 1 / Enhancement semantics | SRS wall kicks; one hold per active piece, replenished after lock; replacement spawns at its initial orientation. Hold and restart do not carry a partially elapsed lock timer into the new piece. | Agent proposal preserving predictable input | Scopes 2–6; proposed |
| 1 / Midline | Show the dynamic ghost only when every projected cell is in the lower half. A straddling projection is hidden; for a 20-row board the lower half is rows 10–19 with zero-based indices. | Conservative whole-piece interpretation of upper/lower half | Scopes 3–6; proposed |
| 1 / Lock timing | Start one full interval when grounding begins. Grounded moves/rotations and repeated hard drops do not extend it. Leaving support cancels the grounded timer; a later touchdown starts a full interval. Freeze gameplay time while suspended/hidden; no catch-up on return. Hard drop to an already grounded position retains elapsed time. | Agent proposal to avoid unlimited grounded resets and background surprises | Scopes 2–6; proposed |
| 1 / Penetrator hold and lifecycle | Disable hold while penetrator is active. Activation spends exactly one bonus, cannot be toggled off/refunded and ends on lock or game over. Holding an ordinary piece retains ordinary hold rules; no stored penetrator state exists. Restart clears bonuses. | Agent proposal consistent with previously expressed penetrator preference; awaiting this project's acceptance | Scopes 4–6; proposed |
| 1 / Penetrator landing safety | Traverse occupied rows without changing settled cells. Use one lowest-valid-landing calculation for gravity, hard drop and ghost. Never merge an overlapping transient position. Reject activation/movement/rotation if it leaves no in-bounds non-overlapping landing at or below the candidate position; do not spend a bonus for rejected activation. Activation is not a timer-reset action; recalculate grounding if its landing changes. | Agent proposal resolving overlap/locking and stranded-piece ambiguity | Scopes 4–6; proposed |
| 1 / Midgame settings | Visibility, preview and action availability change immediately. Turning hold off retains the held slot; re-enabling does not reset hold eligibility. Snapshot the two locking policies for each new active piece; changes apply on next spawn, including hold replacement. Configuration does not reset the board, score, bonuses or timers. | Agent proposal avoiding retroactive timing changes | Scopes 5–6; proposed |
| 1 / Defaults | Ghost dynamic, hard drop on, preview on, hard-drop locking follows general, general full-interval, hold on. The new configurable defaults preserve the previously delivered behavior. | Agent proposal; preview first appears in scope 5 | Scopes 5–6; proposed |
| 1 / Invalid settings | Validate each source independently. Invalid URL value falls through to valid cookie/default without overwriting the cookie. Invalid cookie falls through to default. Duplicate instances of the same setting parameter are invalid rather than guessed. Preserve unrelated query parameters and fragments; URL changes use history replacement. | Agent proposal for deterministic, non-destructive resolution | Scope 6; proposed |
| 1 / Persistence resilience | Use per-setting cookies with a one-year lifetime, Path=/ and SameSite=Lax; Secure on HTTPS. Persist valid explicit URL values, including defaults. If cookies or URL updates are unavailable, keep the game/settings usable in memory and retain whichever persistence channel works. Cookie scope assumes one game instance per origin path policy; no game-state persistence is requested. | Agent proposal; deployment details can be refined before implementation | Scope 6; proposed |
| 1 / Browsers and verification | Follow BROWSER_DEV_POLICY.md: isolated Chromium primary and managed Firefox secondary, headless interaction/rendering sufficient. No browser installation is needed for documentation. Later tasks must provision and prove actual harness capability before dependent acceptance; do not silently remove a required browser. | Existing repository policy; proposed Playwright harness | All scopes; policy active, harness proposed |
| 1 / Versions and releases | First verified classic release v0.1.0; later additive pre-1.0 delivery phases increment minor versions, repairs patch versions. Plan the exact version/phase mapping when scope arrives. Publish release/tag/notes after each authorized, verified and integrated implementation phase. No documentation-only release or initial preparation tag. | Explicit user release instruction; agent version recommendation | Future implementation; proposed mapping, release obligation active |

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
| DOCS-001 | Four root files preserved byte for byte against initial commit 893cffb7da0ac90abadb469c7e117a085e8286f3; no copies needed. Task template copied with only DOCS-001 checked. Initialization commit publication and issue #1 closure require readback after this commit. |
| DOCS-002 | Pass 1 PROJECT proposal pending; first human approval required. |
| DOCS-003–008 | Not started; scoped mode preapproval becomes operative after initial PROJECT approval. |
| DOCS-009 | Not selected; remains unchecked and open at final autoloop stop. |

Material decision status: the product/interaction recommendations above are proposed for first PROJECT approval. Implementation packages, exact key mapping and detailed acceptance fixtures remain for downstream owners. Future scope is not part of the initial PROJECT.

## Initialization and current reset

- Original root presence: all four existed — AI_DISCLOSURE.md, SDD-MANAGER.md, AGENTS.md and SKILL_DISCOVERY_PROTOCOL.md. Retained all four; copied none. Compared bytes with initial Git blobs; preservation passed. All-present initialization adds no continuation pause.
- Package: bundled SDD Manager 0.15.2 at initial commit. Coordinator and initialization/tracking assets match the installed running package after newline normalization; copies use repository package bytes.
- Manual provenance: default enabled. Seed 44373f66c78be757a9455effcf61ad85743c1945 on design-docs/ai-logs from main at 893cffb7da0ac90abadb469c7e117a085e8286f3; explicit two-parent merge 62169f0ad3764882e22400b4881903758c88d94b on main. Both pushes/readbacks matched with confirmed cleanup. Both scaffold files byte-match package assets. No transcript created.
- Branch: design-docs/main created from main at 62169f0ad3764882e22400b4881903758c88d94b; target main. Existing branch and root instructions retained.
- Credentials: repository-local conventional credential is excluded by *.tkn and untracked; no secret belongs in tracked records.
- Current reset: none. Prior passes: none.

## Pending transitions

Publish/read back this initialization commit, then add evidence and close/read back DOCS-001 issue #1. Only afterward prepare/publish the pass-1 PROJECT proposal and README links. First PROJECT acceptance remains pending; hold ARCHITECTURE and all later product documents.
