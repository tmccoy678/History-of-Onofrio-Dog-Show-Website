# Note to the onofrio.com team: unhandled errors on the show-lookup pages

**Date:** October 6, 2026
**From:** Taylor McCoy (longtime exhibitor, onofrio.com user for ~a decade)
**To:** customer.service@onofrio.com
**Subject:** Small robustness issue on onofrio.com show pages — malformed input causes server errors

---

Hello,

I'm writing as a longtime user of onofrio.com — I genuinely love the site and have used it to enter shows for about ten years. I noticed a small issue while browsing and wanted to pass it along so it can be fixed before someone less friendly finds it.

## What I found

The show-lookup pages (URLs starting with `www.onofrio.com/execpgm/fndindex?show=...`) return an **HTTP 500 Internal Server Error** when the `show` parameter is missing, empty, or contains a value that doesn't match a real show — for example:

- `execpgm/fndindex?show=TEST` → 500
- `execpgm/fndindex?show=` (empty) → 500

A valid show code (e.g. `show=PL2026101411BH`) returns the normal page (HTTP 200), and the page with no parameters at all also loads fine (HTTP 200). So the error path is specifically unvalidated `show` values reaching the backend and failing unhandled.

## Why it matters

- Right now the 500 page is generic (no stack traces or paths leak — good), but an unhandled error on every malformed request means malformed input is reaching your backend program without validation. That's the layer worth hardening.
- Automated scanners and curious visitors hit URLs like this routinely. A clean 404 or a friendly "show not found" page would close the issue and look more professional.

## Suggested fix

Validate the `show` parameter before it reaches the backend program: if it's empty or doesn't match the expected show-code format, return a normal 404 or a "show not found" page instead of letting it through to cause an unhandled error.

## The good news

I checked, and the error page itself doesn't disclose anything sensitive — no paths, no stack traces, no backend details. This is purely a robustness/hardening suggestion, not an emergency.

Thank you for maintaining the site — it's a piece of internet history and I mean that as a compliment. Happy to provide more detail if it's useful.

— Taylor
