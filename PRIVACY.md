# Privacy

**Aneirin makes zero network calls of its own. Nothing leaves your machine.**

That is the whole policy. The rest of this page just explains *why* that is true, so you can verify
it rather than take our word for it.

## What stays on your machine

- **Your prompts and code.** Aneirin reads your AI requests in order to optimize them, then forwards
  them to the *same* provider endpoint your editor was already going to call. It is a pass-through on
  `localhost`. It never copies them anywhere else.
- **Your savings counts.** The token-savings numbers shown in the dashboard are written to local log
  files in your Aneirin folder (`wire_ledger.jsonl`, `state.json`). They are never uploaded.
- **Your licence.** Activation is **local-only**. When you paste a licence, Aneirin verifies its
  signature *on your machine* against an embedded public key. It does **not** call a licence server,
  and Aneirin keeps working offline. (There is no "call home to check if you still paid".)

## What Aneirin does NOT do

- It does **not** send your prompts, code, files, traffic, or usage anywhere.
- It does **not** contain analytics, telemetry, crash reporting, or "anonymous usage" pings.
- It does **not** require an account or login to run.
- It does **not** phone home to validate your licence.

## The only network traffic involved

The only outbound connection is the **one your editor was already making** — to your AI provider
(Anthropic / GitHub Copilot) — which now passes through Aneirin's local proxy on the way out. Aneirin
adds no destinations of its own.

There is exactly one *optional, manual, off-by-default* exception: if you personally run
`node version_check.js --online`, it will fetch a single version file from our public GitHub release
page so you can see whether a newer build exists. It sends nothing about you — just an HTTP GET — and
it never runs unless you type that command yourself.

## How to verify

- Watch your own outbound connections (e.g. a firewall or `netstat`) while Aneirin runs: you will see
  connections to your AI provider and **nothing to an Aneirin server**, because there isn't one.
- The savings logs are plain files in your Aneirin folder — open them.
- Activation works with your network disconnected.

---

*If we ever change this — we don't intend to — it would be stated here and in the release notes
before any build that does so.*
