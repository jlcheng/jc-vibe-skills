---
name: wrangler
description: Walk through adding, promoting, installing, updating, and removing skills and plugins in Claude Code and Codex.
disable-model-invocation: true
---

# Wrangler

[workflow.md](workflow.md) is John's own write-up of how he plans to manage skills and plugins
across Claude Code and Codex. Read it for the mechanics of the current task. The user's request
and workspace instructions determine the chosen source, ownership and installation scope; keep
those decisions when applying the workflow. Speak plainly and give the next useful step.
Keep answers short without leaving out either tool.

- Use the skill home John has chosen. Vibe means
  `~/privprjs/jc-vibe-skills/plugins/jc-vibe/skills/<name>/`; provide that path when vibe is
  already chosen. Only an unresolved home calls for a choice between vibe, published and
  third-party ownership; uncertainty leads to recommending vibe. Temporary testing does not
  decide ownership, and installed caches are never source files.
- “How do I” asks for usable instructions. “Install”, “help me install”, “test”, and action
  follow-ups ask you to carry out the work and verify it within the existing authorization.
  Ask only for consequential missing choices. If a catalog has several plugins and no selection,
  name the choices and ask which one John intends before choosing an install command.
- For an explicit plugin installation request, run the supported `jc-plugin install <source>
  [plugin]` operation even when the inventory already lists it; the supported operation handles
  existing installations. Do not substitute a status check for the requested action or remove
  an existing plugin just to create an empty starting state.
- Finish an installation action by checking installed content and a harmless skill invocation in
  fresh sessions of both tools. Read [testing.md](testing.md) for this verification. Avoid setup
  skills or unrelated configuration changes merely to prove loading; report any blocked check.
- For installation questions and actions, first check `jc-plugin list`, inspect the source
  catalogs and complete plugin manifests, and check that each referenced skill path exists.
  Manifest path strings alone are not a file check. This preflight applies to both advice and
  action requests, including unresolved multi-plugin choices and local directories. A plugin
  includes its manifest entries, not necessarily every skill folder. Then identify its packaging
  case in the write-up.
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
- `jc-plugin list` establishes plugin state only. A missing plugin does not establish that
  all its skills are absent: standalone copies may exist. For a named-source comparison,
  inspect that source and compare its actual skills against both plugin and standalone
  installations. Disabled plugins are unavailable; explicit-only skills remain callable.
  See the workflow's inventory section for discovery and the scope of skill overrides.
- For standalone installation, honor the project or personal scope already specified in the
  request or workspace. Copy or link the complete chosen skill folder, preserving resources;
  a project-scoped request must not create personal installations. Project standalone skills
  use `.claude/skills/` and `.agents/skills/`; the personal equivalents are `~/.claude/skills/`
  and `~/.agents/skills/`. Read [testing.md](testing.md) for discovery and behavior checks,
  and preserve test evidence before removing scratch files.
- Skill testing means fresh sessions in **both Claude Code and Codex**, even when John asks
  from just one of them. Read [testing.md](testing.md) for loading, invocation, behavior checks,
  and stale-copy diagnosis. An ordinary skill folder needs no plugin or publication to test.
  For generic advice use candidate placeholders; for execution obtain its path if missing.
  Invoking Wrangler does not identify Wrangler as the candidate being tested.
- Report installation, loading, and behavior as separate evidence. A command that failed in
  one tool is a partial failure, not success in both.
- If what you find contradicts the write-up, tell him, so he can update it.

When John asks to update Wrangler itself, he authorizes editing its source repository,
committing and pushing the changes to GitHub, and refreshing `jc-vibe` in both tools.
Follow the source repository's release instructions and verify with `jc-plugin list`;
no separate confirmation is needed for these steps.
