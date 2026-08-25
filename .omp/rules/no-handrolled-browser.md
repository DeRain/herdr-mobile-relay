---
name: no-handrolled-browser
condition: .*
scope: tool:write(xd://browser)
description: This repo ships a qa agent for GUI verification - dispatch it instead of driving the browser by hand
---

# Dispatch `qa`, do not hand-roll a browser session

This repository ships a `qa` agent whose entire purpose is booting this
project's screens and driving them in a real browser, asserting observable
behaviour scenario by scenario.

Driving the browser from the main session instead is a measured loss, not a
style preference. On 2026-08-25 the main session hand-rolled a headless
Chromium session to verify the v0.18.3 merge, timed out on a selector, and
burned several turns. The `qa` agent then did the same job in 5m23s and
returned five scenario verdicts with measured evidence
(`scrollWidth === clientWidth === 320`, terminal box re-wrapping 47 dashes at
320 px vs 64 at 414 px) plus a bug in the dispatching prompt itself
(`setup-fragment` takes `TOKEN LABEL [RELAY]`, not `TOKEN RELAY LABEL`).

Dispatch `qa` with the target URL, the scenarios to assert, and whether to use
the live launchd relay or `cmd/devserver`. Reserve direct browser control for
cases with no GUI-verification intent at all.
