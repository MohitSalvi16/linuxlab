# Privacy policy

**Last updated:** 2026-07-28

## Summary

LinuxLab collects nothing, sends nothing and has no servers. Everything you type
stays in your browser profile.

## What is stored, and where

| Data                                            | Storage                | Leaves your device?                |
| ----------------------------------------------- | ---------------------- | ---------------------------------- |
| Virtual filesystem (your files and directories) | IndexedDB (`linuxlab`) | No                                 |
| Command history                                 | IndexedDB              | No                                 |
| Settings (theme, font, prompt, toggles)         | IndexedDB              | No                                 |
| Mission progress and badges                     | IndexedDB              | No                                 |
| AI provider configuration and API key           | `chrome.storage.local` | Only to the provider you configure |

API keys are deliberately kept out of IndexedDB so they are never captured by
filesystem exports or snapshots.

## Network activity

LinuxLab makes **no network requests** in its default configuration. There is no
telemetry, no analytics, no crash reporting and no remote configuration.

The single exception is the optional AI assistant. If — and only if — you enter
your own API key and use `explain`, `fix`, `learn` or `ai`, LinuxLab sends the
following directly to the provider **you** selected:

- your question or the command you asked about
- the current working directory
- up to five recent command lines, for context

Those recent command lines are filtered first. Any call to the assistant itself
is dropped — so `ai key sk-...` is never echoed back — and anything
credential-shaped is replaced with `<redacted>` before the request is built:
`NAME=value` and `--flag=value` where the name mentions a key, token, secret,
password or credential; `Authorization:` headers; and recognisable token shapes
such as `sk-`, `ghp_`, `xox...`, `AKIA...`, `AIza...` and JWTs. Shell history is
where credentials end up, and you get no chance to review a prompt before it
leaves, so the filter errs towards redacting too much.

That request goes straight from your browser to the endpoint you configured;
nothing is proxied through any LinuxLab infrastructure, because none exists. The
provider's own privacy policy then applies. Remove the key at any time with
`ai forget` or **Settings → AI → Forget key**.

## Permissions

| Permission  | Purpose                                  |
| ----------- | ---------------------------------------- |
| `storage`   | Persist settings and AI configuration    |
| `sidePanel` | Open the terminal in Chrome's side panel |

The extension requests no host permissions at install time and cannot read the
pages you browse.

## Sandboxing

The terminal cannot access your real filesystem, processes, network interfaces
or clipboard contents beyond what you explicitly select. Every command operates
on the simulated filesystem inside IndexedDB.

## Deleting your data

- **Filesystem:** Settings → Workspace, or run `rm -r` on what you no longer want
- **History:** `history -c`
- **Mission progress:** `mission reset`
- **Everything:** remove the extension from `chrome://extensions`; Chrome deletes
  all associated storage

## Children

LinuxLab is suitable for all ages and knowingly collects no personal information
from anyone, including children under 13.

## Changes

Material changes to this policy will be noted in `CHANGELOG.md` and reflected in
the date above.

## Contact

Open an issue at <https://github.com/MohitSalvi16/linuxlab/issues>.
