# Clockwise rotation contract

This child of [SPEC](../SPEC.md) owns SRS clockwise kick offsets for C01/C04. B01 defines shape cells/pivots and the screen coordinate convention. Orientation cycles 0 → R → 2 → L → 0. For each rotation, rotate cells locally, then try these anchor offsets in the listed order. Positive y is down. O retains its occupied cells with offset (0,0); it needs no kicks.

| Transition | JLSTZ ordered offsets |
| --- | --- |
| 0 → R | (0,0), (−1,0), (−1,−1), (0,2), (−1,2) |
| R → 2 | (0,0), (1,0), (1,1), (0,−2), (1,−2) |
| 2 → L | (0,0), (1,0), (1,−1), (0,2), (1,2) |
| L → 0 | (0,0), (−1,0), (−1,1), (0,−2), (−1,−2) |

| Transition | I ordered offsets |
| --- | --- |
| 0 → R | (0,0), (−2,0), (1,0), (−2,1), (1,−2) |
| R → 2 | (0,0), (−1,0), (2,0), (−1,−2), (2,1) |
| 2 → L | (0,0), (2,0), (−1,0), (2,−1), (−1,2) |
| L → 0 | (0,0), (1,0), (−2,0), (1,2), (−2,−1) |

Ordinary candidates obey board bounds and settled collision. Penetrator candidates, where that capability applies, obey P02's in-bounds and future-landing feasibility rule. Accept only the first admissible candidate; reject all-five failure without changing orientation/anchor. Zero-offset O rotation never changes cells or extends a lock deadline.

Acceptance uses fixtures for every transition/table, an obstructed first candidate with a later success, left/right/floor boundaries, all-candidate rejection and four-turn cell identity. Verify offsets separately from integration collision/timing; a table-only check does not prove SRS integration.
