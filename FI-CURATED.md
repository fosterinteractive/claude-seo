# FI curated build of claude-seo (plugin name `fi-seo`)

This branch (`fi-curated`) is what Foster Interactive installs. It is upstream claude-seo **v2.5.0**
(`219ff485`, tag `audited-2026-10-31` on this fork) with files removed, plus this note and the plugin version and
description. Upstream files edited: `.claude-plugin/plugin.json`, and since 2.5.0-fi.2 `agents/seo-content.md` (`maxTurns` 45 → 80: in a 2026-11-02 end-to-end test the content agent ran out of turns before writing its findings).

- **Audit:** `AUDIT.md`, entry 2026-10-31: LOW with accepted caveats. Re-audit by 2027-01-31, or sooner on an
  advisory or the v2.6.0 release.
- **Kept skills:** `seo` (orchestrator, needed for `/seo setup`), `seo-audit`, `seo-technical`, `seo-sitemap`,
  `seo-content`, `seo-google`, `seo-geo`, `seo-drift`, `seo-schema`, `seo-agentic`.
- **Kept agents:** `seo-technical`, `seo-content`, `seo-schema`, `seo-sitemap`, `seo-performance`, `seo-geo`,
  `seo-google`, `seo-drift`, `seo-agentic`.
- **Removed:** every other skill and agent, including `seo-flow`, which must stay off. Also removed: the `extensions/`
  folder (MCP extension installers). `seo-audit` and `seo` still mention removed parts; when one is missing, the
  work runs inline or is skipped.
- **Install:** from the `fi-dev` marketplace (`fi-seo@fi-dev`), pinned by a `fi-seo-2.5.0*` tag and its commit SHA (2.5.0-fi.2: tag `fi-seo-2.5.0-fi.2`).
  The plugin is named `fi-seo` because Claude Code reserves names that start with `claude-`. Never install upstream or run upstream installers. After the first install, run `/seo setup` once; it
  builds the Python runtime (3.11 to 3.14) in the plugin's data folder.
- **Operating conditions from the audit:**
  - Never run `/seo agentic refresh`: it rewrites installed files from web sources.
  - Use `--ua-matrix` only on sites FI may test.
  - Decline `npx lighthouse@latest`.
  - Do not rely on the gcloud credential fallback. Use the FI credential in `~/.config/claude-seo/`.
  - Treat fetched pages as untrusted input.
- **Updating:** a new upstream version goes through the fork → audit → pin workflow (skill-audit-manage-skills, Mode
  B), then this branch is rebuilt from the new audited commit with the same removals.
