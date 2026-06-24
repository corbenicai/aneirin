# Aneirin

**Use fewer tokens, losslessly.** Aneirin is a local proxy that cuts the token cost of
Claude Code and GitHub Copilot — on your own machine, with your own account, without
changing a single answer the model gives you.

In development on one machine, Aneirin has **physically removed 652 million billed tokens**
from real requests so far — redundant context the model never needed to see again. Same
answers, smaller bill.

> [!NOTE]
> **Lossless** means the model receives everything it needs to answer correctly. Aneirin
> only trims context that is redundant or re-billed — never the meaning of your request.

---

## Why Aneirin

- **Lossless** — identical model behaviour; it removes re-billed context, not information.
- **Local** — runs on `127.0.0.1`. There is no Aneirin server in the path.
- **No phone-home** — zero network calls of its own. Your prompts, code, and counts never
  leave your computer.
- **Your own account** — it only optimizes traffic you're already authorized to send.
- **Zero workflow change** — keep using Claude Code and Copilot exactly as you do today.
- **Fully reversible** — one command uninstalls it; a kill-switch flips it to pure
  pass-through instantly.

## How it works

1. Aneirin runs a small proxy on `localhost`; your editor's AI traffic passes through it.
2. For each outgoing request it applies **lossless** reductions:
   - removes your own previous turns' "thinking" blocks the model no longer needs,
   - de-duplicates byte-identical context that would otherwise be re-sent,
   - places prompt-cache markers where the provider caches most effectively.
3. It forwards the slimmer request to the same provider endpoint your editor already used.
4. If anything goes wrong inside Aneirin, it forwards your **original** request untouched
   (fail-open) — it never blocks or corrupts a request to "save" tokens.

The biggest single lever is removing stale prior-turn reasoning. In one real request,
Aneirin stripped **399,906 tokens** of prior thinking from a single call — content the model
had already used and didn't need resent.

## What "lossless" means (the guarantee)

| Preserved exactly | Removed / relocated (never billed twice) |
|---|---|
| Your current question and instructions | Prior-turn "thinking" the model already consumed |
| Tool calls and their results | Byte-identical context repeated across turns |
| The frontier (latest) turn, in full | Cache markers moved to better boundaries |

Aneirin's losslessness is checked against a suite of **real captured transcripts** (including
interleaved-thinking and multi-turn tool use) — every transformation is asserted to leave the
model-visible content byte-identical before it ships.

> [!IMPORTANT]
> **Privacy.** Aneirin makes no network calls of its own and contains no telemetry. Your
> prompts, code, traffic, savings counts, and licence stay on your machine. The licence is
> verified **locally** — there is no licence server and no "call home to check if you paid."
> It keeps working offline.

## Measure it yourself

Aneirin ships with a local dashboard and a savings ledger. It only counts **provably removed**
tokens (the ones it physically deleted from a request) — not estimates. You can watch your own
saved total grow and verify the numbers against your provider's usage page. Nothing is uploaded
to produce them.

## Supported

| | |
|---|---|
| Claude Code | ✅ VS Code and CLI |
| GitHub Copilot | ✅ VS Code and CLI |
| OS | Windows today; macOS and Linux to follow |
| Account | your own — no shared or pooled access |

## Pricing

| Tier | Price | What you get |
|---|---|---|
| **Free** | $0 | The full optimizer, capped at **5 million optimized tokens per day** (combined across projects). Dashboard and ledger always on. |
| **Pro — Monthly** | **$5 / month** | No daily cap. Cancel anytime. |
| **Pro — Lifetime** | **$75 once** | Everything in Pro, never expires, one machine. |

For a token-heavy developer the lifetime licence typically pays for itself within about a
month — and the dashboard shows you exactly how much you've saved.

## FAQ

**Does it change the answers I get?**
No. It removes context the model has already used or that is byte-for-byte repeated, and
relocates cache markers. The model's input meaning is unchanged; output behaviour is the same.

**Why is it closed-source?**
The optimizer is the product. In place of "read the code," Aneirin earns trust by being
local, making no network calls of its own, verifying its licence offline, and being fully
reversible with a one-command uninstall.

**Can I trust a proxy with my prompts?**
Everything stays on your machine — the proxy binds to `127.0.0.1` only and forwards to the
same endpoint your editor already called. There is no Aneirin server to send anything to.

**What if it breaks something?**
It fails open: on any internal error it forwards your original request untouched. You can also
drop a kill-switch file to make it pure pass-through instantly, or uninstall in one command.

**Is this allowed by my provider?**
You're optimizing your own authorized traffic with a local tool. A full plain-language note on
what Aneirin does and the responsibilities involved ships alongside the product.

## Status

Preparing for public release. Signed binaries, install instructions, and the purchase flow are
on the way — this page will be updated when they land.

---

© Corbenic AI, Inc. Aneirin is provided as-is; you are responsible for your own use of it under
your provider's terms.
