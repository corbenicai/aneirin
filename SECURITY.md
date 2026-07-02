# Security Policy

We take the security of Aneirin seriously. Aneirin runs on your own machine,
works with your own AI account, and touches your HTTPS traffic locally, so we
want reports of any problem to reach us quickly and privately.

## Supported versions

Only the **latest release** is supported with security fixes. Please always run
the newest version from the
[Releases page](https://github.com/corbenicai/aneirin/releases/latest).

## Reporting a vulnerability

**Please do not open a public GitHub issue for a security problem.**

Report it privately in one of these two ways:

1. **Email:** send the details to **sietse@corbenic.ai**.
2. **GitHub:** use "Report a vulnerability" under the repository's **Security**
   tab (private vulnerability reporting).

Please include:

* A clear description of the problem and why it is a risk.
* Steps to reproduce it, if you can.
* The Aneirin version and your operating system.

Please do **not** include private prompts, code, or personal secrets.

### What to expect

* We aim to acknowledge your report within **3 working days**.
* We will keep you updated while we investigate.
* Once a fix is released, we are happy to credit you (only if you want).

We ask that you give us a reasonable chance to fix an issue before sharing it
publicly.

## How Aneirin is designed to be safe

For context, these are the security properties Aneirin is built around:

* **Runs locally.** The proxy binds to `127.0.0.1` only. It is not reachable
  from the network.
* **No phone home.** Your prompts, code, and usage never leave your machine.
  Free and Lifetime make zero network calls. A Monthly licence does one thing:
  once a day it refreshes its own licence by sending only a device id.
* **Your own certificate.** To optimize your HTTPS traffic, Aneirin generates a
  local certificate **on your computer**. It is unique to you and is never
  shipped with the product. `aneirin.exe uninstall` removes it.
* **Only your provider hosts are touched.** Aneirin only decrypts traffic to the
  AI provider endpoints it optimizes. Everything else passes through untouched.
* **Fails open.** If anything goes wrong internally, Aneirin forwards your
  original request unchanged. A kill switch and one command uninstall are always
  available.

## Checking your download

Each release includes a `SHA256SUMS` file. You can compare the SHA-256 of your
downloaded file against it to confirm the download was not altered.

Note: the Windows binary is currently **unsigned**, so Windows may show an
"unknown publisher" prompt on first run. This is expected for new independent
software. Verifying the SHA-256 checksum is the reliable way to confirm the file
is genuine.
