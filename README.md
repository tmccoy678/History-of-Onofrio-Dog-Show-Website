# Onofrio / InfoDog Computing History Research

Private research notes on the computing history of the two great AKC dog-show
superintendent websites — **onofrio.com** (Jack Onofrio Dog Shows, Oklahoma City OK)
and **infodog.com** (MB-F, Inc., Greensboro NC) — and their lineage back to the
IBM AS/400 era.

Researched October 2026 by Taylor McCoy, with Nova.

## Contents

- [HISTORY.md](HISTORY.md) — the AS/400 lineage, company background, Wayback archaeology
- [FINDINGS.md](FINDINGS.md) — the `execpgm/` discovery: the old backend is still live
- [TESTS.md](TESTS.md) — robustness tests performed on the show-lookup endpoints
- [REPORT.md](REPORT.md) — the disclosure report sent to Onofrio (2026-10-06)
- [evidence/](evidence/) — archived page captures

## The one-line version

onofrio.com's live URLs still call `execpgm/` — "execute program" — a web gateway
reaching straight through to backend programs descended from the original AS/400
system. The old machine is still in there, behind the Apache, in 2026.
