# Onofrio / InfoDog Computing History Research

I became interested in the history of the popular dog show websites, onofrio.com and infodog.com, and decided to publish my findings. I am intrigued by the possibility that Onofrio was built for an AS/400, and I wonder if the machine is still at their HQ. The InfoDog website was likely built for computer whose company no longer exists! I would love to see the original computers someday. 

Onofrio is one of the largest and oldest dog show entry services, and among the first to use the internet to allow people to enter their dogs in AKC shows online. I have found forum posts from the late 90s discussing the architecture of the website. InfoDog shares the same history, but a different UI and choice of software engineering practices since the computer it was built for was not an IBM machine. 

Thankfully, great care was taken to build the websites by hand, pre-AI, and some of the oldest pages are now true relics in the field of the history of technology and computing. 

Who built the original websites? Where are the original machines? 

Private research notes on the computing history of the two great AKC dog-show
superintendent websites — **onofrio.com** (Jack Onofrio Dog Shows, Oklahoma City OK)
and **infodog.com** (MB-F, Inc., Greensboro NC) — and their lineage back to the
IBM AS/400 era.

Researched October 2026 by Taylor McCoy, with Meta's Muse AI and Codex-CLI (Cyber, Astra, GPT-5.6 sol).

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
