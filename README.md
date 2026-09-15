# copilot-plugins

A **generic marketplace index** for [Pietro Di Bello](https://github.com/xpepper)'s
GitHub Copilot CLI plugins. This repository is the index, not the plugins: it holds
only the marketplace manifest (`.github/plugin/marketplace.json`) and this README.

## Hosting model

- Real plugins live in **their own repositories** and are referenced here with the
  external source form (`{"source": "github", "repo": "owner/repo", "path": "..."}`).
  Installing a plugin from this marketplace installs it **from its own repository**, pinned to the release tag named by the entry's `source.ref` (ref pinning verified honored by `copilot plugin install/update`).
- `./plugins/<name>` directories in this repository are **reserved for small,
  self-contained packs** that are not worth a repository of their own. None yet.
- Both forms may mix, as GitHub's own marketplace does.

## Use it

```sh
copilot plugin marketplace add xpepper/copilot-plugins
copilot plugin install gem-pr-review@xpepper-copilot-plugins
copilot plugin install z-pr-review@xpepper-copilot-plugins
```

The marketplace name is `xpepper-copilot-plugins` (the manifest's `name`
field): a marketplace literally named `copilot-plugins` is rejected by the
CLI because it collides with the built-in default marketplace of the same
name (verified live 2026-09-13, Copilot CLI 1.0.83).

(Extensions currently need `--experimental` when starting Copilot CLI; see each
plugin's repository.)

## Indexed plugins

| Plugin | Version | Source |
| --- | --- | --- |
| [copilot-pr-review](https://github.com/xpepper/copilot-pr-review) | 0.1.0 | [xpepper/copilot-pr-review](https://github.com/xpepper/copilot-pr-review) (root, tag `v0.1.0`) |
| [gem-pr-review](https://github.com/xpepper/pr-review-gemini) | 0.4.0 | [xpepper/pr-review-gemini](https://github.com/xpepper/pr-review-gemini) (root, tag `v0.4.0`) |
| [z-pr-review](https://github.com/xpepper/pr-review-glm) | 0.2.7 | [xpepper/pr-review-glm](https://github.com/xpepper/pr-review-glm) (root, tag `v0.2.7`) |

Parallel, multi-lens AI code review for GitHub pull requests, built on the
Agent Plugins 1.0 standard (`gem-pr-review`): parallel review lenses,
host-gated publication of findings.

Parallel tiered pull-request review for GitHub Copilot CLI (port of
[pi-pr-review](https://github.com/10ego/pi-pr-review)): code-owned gates,
host-validated findings, gated COMMENT publication.

## Versioning discipline

Every plugin release that bumps its own `plugin.json` version also bumps the
matching entry version here (one-line change). The plugin's own repository
gate-checks this consistency (`tests/smoke-m1.mjs`), so a skipped bump fails
its next assessment.
