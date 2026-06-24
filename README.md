# Aneirin

**Use fewer tokens, losslessly.** A local optimizer for the AI API traffic you're already
authorized to use — Claude Code and GitHub Copilot, on your own machine, with your own account.

> Status: preparing for public release. Binaries and install instructions are on the way.

---

## What it does

Aneirin runs a small proxy **on your own computer** (localhost). Your editor's AI traffic
passes through it on the way out, and Aneirin rewrites each *request* so it carries the same
meaning with fewer billed tokens — mainly by:

- removing your own previous turns' "thinking" blocks the model no longer needs to see,
- de-duplicating byte-identical context that would otherwise be re-sent,
- placing prompt-cache markers where the provider caches most effectively.

The model still receives everything it needs to answer correctly. We call this **lossless**:
the content the model acts on is unchanged — only redundant, re-billed material is trimmed.
If anything goes wrong inside Aneirin, it forwards your original request untouched (fail-open),
so it never blocks or corrupts a request to "save" tokens.

## Why you can trust it

- **Runs locally.** Everything happens on your machine. There is no Aneirin server in the path.
- **No phone-home.** Aneirin makes zero network calls of its own. Your prompts, code, traffic,
  counts and licence never leave your computer.
- **Your own account, your own keys.** It only optimizes traffic you're already sending.
- **Lossless.** It trims redundant, re-billed context — not the meaning of your request.
- **Fully reversible.** One command uninstalls it and restores normal traffic. A built-in
  kill-switch turns the engine into pure pass-through instantly.

## Pricing

| Tier | Price | What you get |
|---|---|---|
| **Free** | $0 | The full optimizer, capped at **5 million optimized tokens per day** (combined across projects). Dashboard + savings ledger always on. |
| **Pro — Monthly** | **$5 / month** | No daily cap. Cancel anytime. |
| **Pro — Lifetime** | **$75 once** | Everything in Pro, never expires, one machine. |

For a token-heavy user, the lifetime licence typically pays for itself within about a month —
and the dashboard shows you exactly how much you've saved.

## Privacy & licensing

Aneirin's licence is verified **entirely on your machine** — there is no licence server and no
"call home to check if you still paid." A licence is tied to one computer.

A full privacy statement and a plain-language note on what Aneirin does (and the responsibilities
that come with optimizing your own traffic) ship alongside the product.

---

© Corbenic AI, Inc. Aneirin is provided as-is; you are responsible for your own use of it under
your provider's terms.
