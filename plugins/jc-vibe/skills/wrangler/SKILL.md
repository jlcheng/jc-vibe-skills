---
name: wrangler
description: Walk through adding, promoting, installing, updating, and removing skills and plugins in Claude Code and Codex.
disable-model-invocation: true
---

# Wrangler

[workflow.md](workflow.md) is John's own write-up of how he plans to manage skills and plugins
across Claude Code and Codex. Read it for the mechanics of the current task.

- Resolve a multi-plugin source's selection before supplying installation commands or executing
  them. If John has not selected a plugin, name the available choices and ask which he wants. A list
  of install commands for all plugins does not resolve that choice. Ask only for consequential
  missing choices; keep selections already made.
- For an explicit plugin installation request, run the supported
  `jc-plugin install <source> [plugin]` operation. `<source>` is a repository URL, owner/repository
  or local marketplace path, never the `plugin@marketplace` identity printed by `list`. Use
  `update <plugin>` for a version refresh.
- For installation questions and actions, first check `jc-plugin list` to see what is already
  installed.
- Prefer `jc-plugin` when the repo packages skills inside plugins. `npx skills` installs skills as
  files without plugin namespacing.
- Codex accepts Claude plugin packaging: `.claude-plugin/marketplace.json` and
  `.claude-plugin/plugin.json`, including a `skills` array. Separate Codex files are not required.
  This compatibility was verified by installing `mattpocock-skills@mattpocock` 1.2.3 with Codex CLI
  0.157.1 on 2026-09-26. `jc-plugin` supports Claude-only catalogs too; use
  `jc-plugin install <source> [plugin]`.
- `jc-plugin list` establishes plugin state only. A missing plugin does not establish that all its
  skills are absent: standalone copies may exist.
