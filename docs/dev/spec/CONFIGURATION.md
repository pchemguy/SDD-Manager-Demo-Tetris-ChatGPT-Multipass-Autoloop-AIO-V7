# Configuration contract

This child of [SPEC](../SPEC.md) owns validated selected settings for C10, their browser controls and the persistence schema where applicable. Lock settings are selected values; each active piece has its own effective snapshot. All domains are case-sensitive exact strings without coercion.

| Setting | Allowed values | Default | Application timing |
| --- | --- | --- | --- |
| ghost | hide / dynamic / show | dynamic | Immediate; hide suppresses only drawing, show ignores midline, dynamic follows V01 |
| hardDrop | 0 / 1 | 1 | Immediate action availability |
| next | 0 / 1 | 1 | Immediate preview visibility; no draws |
| hardDropLock | general / immediate | general | Next active piece |
| lock | failed / interval | interval | Next active piece |
| hold | 0 / 1 | 1 | Immediate availability, still gated by eligibility and penetration |

Use labeled native select/checkbox controls with visible selected values and keyboard focus. Boolean controls map only to canonical 0/1 values at the codec boundary. Reject unknown keys or values without mutation; a malformed control intent changes neither game nor settings. Display a short note that locking changes apply to the next piece. They do not clear a current timer. A hold replacement is a new active piece; a no-op/rejected hold is not. Changing visibility while suspended redraws without advancing time.

Selected configuration belongs to the page, independent of Game. Restart retains it. In a fresh page initialize all six fields to defaults before the first run. There is no persistence of score, source queue, bonuses, hold slot, active piece or deadlines.

## Session boundary

Do not read/write configuration cookies, local/session storage or URL query parameters. Reload initializes all six defaults even if a URL/cookie happens to contain similarly named data. Changing a control leaves the URL and browser storage untouched. Test both restart retention and reload reset; they are different boundaries.
