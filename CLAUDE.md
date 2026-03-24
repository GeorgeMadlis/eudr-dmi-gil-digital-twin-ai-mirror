# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Four-Repo Project Overview

This repo is one of four that form the EUDR evidence platform, all under the `georgemadlis` GitHub account:

| Repo | Role |
|------|------|
| **eudr-dmi-gil-digital-twin-ai-mirror** ← (this repo) | Read-only CI-managed mirror of the Digital Twin for AI inspection |
| **eudr-dmi-gil-digital-twin** | Source — this repo is force-pushed from there on every `main` push |
| **eudr-dmi-gil** | Authoritative report generation |
| **eudr-client-portal** | Private web portal |

---

## Purpose and Usage

This repo is a **static, force-pushed mirror** of `eudr-dmi-gil-digital-twin/docs/site/`. It exists so AI inspection engines and automated tools can access the Digital Twin's published artifacts directly from GitHub without going through GitHub Pages DNS resolution or Cloudflare.

**Do not commit to this repo manually.** All content is managed by the `publish-ai-mirror` CI workflow in `eudr-dmi-gil-digital-twin`.

### When to use this repo
- Use `site/aoi_reports/runs/<run_id>/aoi_report.json` to read structured AOI report data
- Use `site/aoi_reports/runs/<run_id>/report.html` to read rendered report HTML
- The content here always reflects the last pushed state of the Digital Twin

### Canonical URLs
The live public site is at:
```
https://georgemadlis.github.io/eudr-dmi-gil-digital-twin/site/
```
Use the mirror for programmatic access; use the GitHub Pages URL for human-readable browsing.

---

## How the Mirror Is Updated

In `eudr-dmi-gil-digital-twin`, `.github/workflows/publish-ai-mirror.yml`:
1. Renders DTE instructions and rebuilds the AOI reports index
2. Validates all site links
3. rsync-copies `docs/site/` into a `mirror_root/site/` staging area
4. Force-pushes `mirror_root/` to this repo's `main` branch

Required secret in `eudr-dmi-gil-digital-twin`: `AI_MIRROR_PUSH_TOKEN` (PAT with write access here).

---

## Content Structure

```
site/
├── aoi_reports/
│   ├── index.html
│   └── runs/
│       ├── example/          # Estonia test AOI
│       ├── se_asia/          # Vietnam example
│       ├── west_africa/      # Ghana example
│       └── latin_america/    # Colombia example
├── dao_reports/
├── dao_dev/
├── dao_stakeholders/
├── dependencies/
├── regulation/
├── views/
└── articles/
```
