# copilot-plugins

A **generic marketplace index** for [Pietro Di Bello](https://github.com/xpepper)'s
GitHub Copilot CLI plugins. This repository is the index, not the plugins: it holds
only the marketplace manifest (`.github/plugin/marketplace.json`) and this README.

## Hosting model

- Real plugins live in **their own repositories** and are referenced here with the
  external source form (`{"source": "github", "repo": "owner/repo", "path": "..."}`).
  Installing a plugin from this marketplace installs it **from its own repository**.
- `./plugins/<name>` directories in this repository are **reserved for small,
  self-contained packs** that are not worth a repository of their own. None yet.
- Both forms may mix, as GitHub's own marketplace does.

## Use it

```sh
copilot plugin marketplace add xpepper/copilot-plugins
copilot plugin install z-pr-review@<marketplace-name>
```

(Extensions currently need `--experimental` when starting Copilot CLI; see each
plugin's repository.)

## Indexed plugins

| Plugin | Version | Source |
| --- | --- | --- |
| [z-pr-review](https://github.com/xpepper/pr-review-glm) | 0.2.4 | [xpepper/pr-review-glm](https://github.com/xpepper/pr-review-glm) (root) |

Parallel tiered pull-request review for GitHub Copilot CLI (port of
[pi-pr-review](https://github.com/10ego/pi-pr-review)): code-owned gates,
host-validated findings, gated COMMENT publication.

## Versioning discipline

Every plugin release that bumps its own `plugin.json` version also bumps the
matching entry version here (one-line change). The plugin's own repository
gate-checks this consistency (`tests/smoke-m1.mjs`), so a skipped bump fails
its next assessment.
