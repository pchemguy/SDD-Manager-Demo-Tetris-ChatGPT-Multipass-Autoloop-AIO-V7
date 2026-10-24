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

## External names and validation

Use query names exactly matching the setting column: ghost, hardDrop, next, hardDropLock, lock, hold. Cookie names are `tetris.` followed by the same key. Decode URL parameters through URLSearchParams; decode cookie values using percent decoding and treat malformed encoding as invalid. Unknown fields are ignored. Duplicate query parameters for one recognized setting invalidate that setting's URL source; duplicate cookie names invalidate that cookie source. No trimming, numeric/Boolean coercion or case folding is performed. An empty recognized value is invalid.

## Startup resolution

Resolve each field separately, before first spawn:

1. If exactly one recognized URL parameter exists and its decoded value is valid, select it and save that exact canonical value to the corresponding cookie, including default-valued selections.
2. Otherwise, if exactly one matching cookie exists with a valid decoded value, select it. An omitted/invalid/duplicate URL value does not overwrite that cookie.
3. Otherwise select the default. Invalid cookies are ignored; do not replace them merely because fallback was needed.

Resolution of one field never chooses the source for another. Startup does not add omitted parameters to the URL, remove invalid/unknown parameters or rewrite unrelated URL content. Valid explicit URL values are saved even if no control is changed. Read failures make that source unavailable, while the other source/default still participates.

## Control-change synchronization

After accepting a control change, update memory once. Attempt its cookie save and its URL update independently; failure of either must not skip the other. Write one cookie `tetris.<key>=<percent-encoded-canonical-value>; Max-Age=31536000; Path=/; SameSite=Lax`, adding Secure on HTTPS. Do not erase other settings cookies. Readback may detect blocked writes; selected memory values remain in force and a concise non-blocking “Settings could not be fully saved” status is allowed.

Build a URL from the current location, set that recognized parameter once (replacing duplicates), preserve other settings, unknown parameters, path and fragment semantically, then use history.replaceState. No page navigation or new history entry occurs. Do not require byte-identical percent encoding/order of unrelated parameters after URLSearchParams serialization. A same-value control intent still repairs/writes that setting's cookie and parameter; no gameplay transition is generated. Do not canonicalize unrelated invalid parameters during a single-field edit.

## Failure and deployment scope

Catch cookie/history access errors per channel. If cookies are blocked but URL updates succeed, reload restores explicit URL settings; if URL updates fail but cookies save, reload restores saved values. If both fail, page-memory settings remain usable until reload. Do not claim durable save from a swallowed error. Use one game configuration namespace per origin because Path=/ shares these named cookies; deploying independent configurations on one origin requires an explicit schema/scope decision. No server, storage permission prompt or external service is necessary.

## Acceptance

Use mixed-source fixtures in one reload: valid URL override, omitted URL with saved non-default cookie, explicit default URL with stale cookie, invalid URL with valid cookie, invalid cookie with no URL, duplicate URL/cookie and unrelated parameters/fragment. Verify exact per-field selected values and cookie writes. Change only one control and observe independent cookie and history attempts plus unchanged other selected settings. Exercise both individual channel failures and both unavailable, including restart retention and successful URL/cookie reload in the actual browsers.
