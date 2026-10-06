# Findings: the AS/400's fingerprints are in the URL bar

## The `execpgm/` gateway

Every show listing on the live onofrio.com (checked 2026-10-06) is served
through URLs of this form:

```
http://www.onofrio.com/execpgm/fndindex?show=PL2026101411BH#FCMU1
http://www.onofrio.com/execpgm/fndindex?page=JP0000000000@@
http://www.onofrio.com/execpgm/index?index=TL
```

`execpgm` reads as "execute program": a web gateway that invokes backend
programs directly. The `show=` values are encoded show identifiers
(`PL2026101411BH` etc.); the `#FCMU1` fragments and `@@` padding are classic
legacy patterns.

The frontend is Apache (`Server: Apache` header). Behind it, something real
executes: requesting `execpgm/fndindex?show=TEST` with a bogus show code
returns **HTTP 500** — an unhandled backend error, not a 404. That is the
sound of a live program catching the input, trying to run it, and choking.
A static site would have nothing to choke on.

## What this means

The web frontend is a thin wrapper around program calls whose lineage traces
to the original AS/400 system. The old machine — or its direct software
descendant — is still executing show lookups in 2026. This is consistent with
the site being maintained by its original engineer: the system was never
rewritten, only fronted.

## Contrast: infodog.com

InfoDog now sits behind AWS Elastic Load Balancing (`Server: awselb/2.0`) and
returns 403 to automated clients. Its infrastructure has been modernized (or at
least re-fronted) in a way Onofrio's visibly has not.

## Cultural footnote

Public reviews (Wanderlog) show outsiders complaining about Onofrio's site
with lines like *"it's 2024, not the 1990s."* They mean it as an insult.
The `execpgm/` URLs suggest the site is, in a real sense, still the 1990s —
and still working.
