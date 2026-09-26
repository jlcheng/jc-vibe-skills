---
name: wrangler
description: Walk through adding, promoting, installing, updating, and removing skills and plugins in Claude Code and Codex.
disable-model-invocation: true
---

# Wrangler

[workflow.md](workflow.md) is John's own write-up of how he plans to manage skills and plugins
across Claude Code and Codex. Read it first, then help him through whichever step he is on. Speak
plainly and offer one step at a time.

- When a new skill comes up, ask which place it belongs in. If he isn't sure, suggest vibe. Don't
  push him to decide more than that.
- When he names someone else's repo, look at it yourself before advising: which catalogs it ships,
  which plugins they list, or whether it has only skill folders. Then say which case in the
  write-up it falls under.
- Prefer `jc-plugin` when the repo packages skills inside plugins. `npx skills` installs skills as
  files without plugin namespacing, losing namespaced commands and allowing names to collide across
  sources. Guide John through `jc-plugin install` for plugin-packaged skills. Use `npx skills` for
  standalone skill folders when its project-copy model is what he wants.
- Codex accepts Claude plugin packaging: `.claude-plugin/marketplace.json` and
  `.claude-plugin/plugin.json`, including a `skills` array. Separate Codex files are not
  required. Inspect the catalog, plugin manifest, and referenced skill paths; do not infer
  incompatibility from missing Codex filenames. This compatibility was verified by installing
  `mattpocock-skills@mattpocock` 1.2.3 with Codex CLI 0.157.1 on 2026-09-26.
  `jc-plugin` supports Claude-only catalogs too; use `jc-plugin install <source> [plugin]`.
- Check current state with `jc-plugin list` rather than assuming what is installed.
- If what you find contradicts the write-up, tell him, so he can update it.

When John asks to update Wrangler itself, he authorizes editing its source repository,
committing and pushing the changes to GitHub, and refreshing `jc-vibe` in both tools.
Follow the source repository's release instructions and verify with `jc-plugin list`;
no separate confirmation is needed for these steps.
