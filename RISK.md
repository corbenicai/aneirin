# What Aneirin does, and what you should know before installing

**One sentence:** Aneirin is a local optimizer that helps you use *fewer tokens, losslessly*, on the
AI API traffic you are already authorized to send — Claude Code and GitHub Copilot, on your own
machine, with your own account.

Please read this before you install. It is short and it is honest.

---

## What it actually does

Aneirin runs a small proxy **on your own computer** (localhost, port 8765). Your editor's AI traffic
passes through it on the way out. Aneirin rewrites the *request* so it carries the same meaning with
fewer billed tokens — mainly by:

- **removing your own previous turns' "thinking" blocks** that the model no longer needs to see,
- **de-duplicating** byte-identical context that would otherwise be re-sent,
- **placing prompt-cache markers** where the provider caches most effectively.

The model still receives everything it needs to answer correctly. We call this **lossless**: the
content the model acts on is unchanged; only redundant, re-billed material is trimmed. If anything
goes wrong inside Aneirin, it **forwards your original request untouched** (fail-open) — it never
blocks or corrupts a request to "save" tokens.

## The honest facts in your favour

These are real, and they are the reason we are comfortable shipping this:

1. **It runs locally.** Everything happens on your machine. There is no Aneirin server in the path.
2. **No phone-home.** Aneirin makes **zero network calls of its own.** It does not send your prompts,
   code, traffic, counts, or licence anywhere. (See `PRIVACY.md`.)
3. **Your own account, your own keys.** Aneirin only optimizes traffic *you* are already sending on
   *your* authorized account. It does not share, pool, resell, or proxy anyone else's access.
4. **Lossless.** It trims redundant/re-billed context, not the meaning of your request.
5. **Fully reversible.** One command uninstalls it and restores normal traffic. There is a
   `DISABLE.flag` kill-switch that turns the engine into pure pass-through instantly, and the
   licence check is local-only — nothing breaks if our website disappears.

## The honest risk you are accepting

Aneirin works by running a **local proxy that modifies your API requests** before they leave your
machine. Provider Terms of Service are written around *normal* client behaviour, and a local
request-rewriter sits in a **grey zone**. To be clear about the realistic worst case:

- A provider *could* consider an automated request-modifier to be outside their intended use, and in
  principle could warn an account or change their API in a way that stops the optimization working.
- We think pushback, if any, would be about the **method** (a proxy that edits requests), not the
  **goal** (using fewer tokens) — no provider can credibly argue that you must be billed for
  redundant tokens. But we are not your lawyer, and we are not promising the provider agrees.

**By installing Aneirin you accept that you are choosing to optimize your own authorized traffic with
a local tool, in a ToS grey area, at your own discretion.** If that is not acceptable to you, do not
install it. If it is, you can remove it completely at any time (see below).

## Removing it

```
# stop and disable instantly (engine becomes pure pass-through):
#   create an empty file named DISABLE.flag in your Aneirin folder
# full uninstall (restores normal traffic, removes the local CA trust we added):
node uninstall.js
```

Uninstall removes the local proxy, undoes the editor proxy settings, and removes the **single**
local certificate Aneirin added so it could see HTTPS traffic on your own machine. It does not touch
anything else.

---

*Aneirin is provided as-is. You are responsible for your own use of it under your provider's terms.*
