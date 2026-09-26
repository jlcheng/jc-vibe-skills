# How I manage my skills and plugins

Written 2026-09-26. This is my plan, not a finished process. I expect to change it as I use it.

I use Claude Code and Codex, and I want the same skills in both. I install, update, and remove
them with `jc-plugin`, which runs each tool's own plugin commands for me.

## Where my skills live

| Place          | Repo                                                                       | What goes there                                                  |
| -------------- | -------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| Vibe           | `jlcheng/jc-vibe-skills` (`~/privprjs/jc-vibe-skills`), plugin `jc-vibe`   | Experiments I don't care much about. Most new skills start here. |
| Published      | `jlcheng/jc-agent-skills` (`~/privprjs/jc-agent-skills`), plugin `jc-code` | Skills I care enough about to publish.                           |
| The real world | Someone else's repo, e.g. `mattpocock/skills`                              | Plugins I use as they are.                                       |

I don't have a rule for vibe versus published. I decide each time. If I'm not sure, it goes in
vibe; I can promote it later.

## The commands

```
jc-plugin list                          # each plugin, with its version in Claude and in Codex
jc-plugin install <source> [plugin]     # source: owner/repo, a Git URL, or a local folder
jc-plugin update <plugin>               # Claude updates in place; Codex removes and re-adds
jc-plugin uninstall <plugin>            # removes it from both
```

`--dry-run` shows what `install`, `update`, or `uninstall` would run, without running it.
`list --all` also shows the plugins Codex installs on its own.

The `plugin@marketplace` value printed by `list` is an installed identity, not an installation
source. To add a missing installation, inspect its source and use `install <source> [plugin]`;
for example, `jc-plugin install https://github.com/mattpocock/skills mattpocock-skills`.
Use the plugin name for `update` and `uninstall`.

Sessions that are already open keep the old version. I start a new session to get the new one.

## Adding or changing one of my skills

1. Edit or add the skill folder under `plugins/<plugin>/skills/` in vibe or published.
2. Follow that repo's `CLAUDE.md`. Both repos make me raise the plugin version in the Claude and
   Codex manifests together. Without a new version, Claude may think nothing changed.
3. For a GitHub release, commit and push to `main`. Test unpushed edits locally first; see
   [Testing skills](testing.md). A local marketplace installation reads your local source.
4. First time: `jc-plugin install jlcheng/<repo> <plugin>`. After that: `jc-plugin update <plugin>`.
5. `jc-plugin list` should show the same new version for Claude and Codex.

## Promoting a skill from vibe to published

1. Move the skill folder from `jc-vibe-skills` to `jc-agent-skills`.
2. Remove its entry from `EXPERIMENTS.md` and add one to `VETTING.md`.
3. Raise the version of both plugins, push both repos.
4. `jc-plugin update jc-vibe`, then `jc-plugin update jc-code`.

Its name changes, from `/jc-vibe:<skill>` to `/jc-code:<skill>`. That's fine.

## Plugins and skills from the real world

Before installing, look at how the repo packages its skills. Prefer `jc-plugin` for skills shipped
inside plugins. `npx skills` installs skill files without plugin namespacing, so it loses
namespaced commands and allows names to collide across sources. That is a major limitation when
using skills from plugins. Use `npx skills` for standalone skill folders when you specifically
want editable files copied into a project. Don't recommend it as the default just because the repo
also documents it.

Then check which catalogs the repo ships:

- **Both a Claude and a Codex catalog** (`.claude-plugin/marketplace.json` and
  `.agents/plugins/marketplace.json`): `jc-plugin install <owner/repo> [plugin]`.
- **Only a Claude catalog.** Codex can read `.claude-plugin/marketplace.json` and the
  `.claude-plugin/plugin.json` it points to, including a `skills` array. Separate Codex files
  are not required. Use `jc-plugin install <source> [plugin]` here too. John verified
  `jc-plugin install https://github.com/mattpocock/skills` on 2026-09-26: both Claude and
  Codex reported `mattpocock-skills@mattpocock` 1.2.3. He then successfully removed it
  from both with `jc-plugin uninstall mattpocock-skills`.
  Inspect the manifest and referenced files to assess the package. Successful installation
  establishes packaging compatibility; it does not verify every skill's behavior.
- **No plugin catalog at all**, just skill folders: install or test the complete chosen folder
  using each tool's standalone skill location. Preserve its scripts and resources. Inspect a
  GitHub checkout just as you would a local folder; a raw SKILL.md alone may omit dependencies.
  See [Testing skills](testing.md). No plugin manifest, marketplace, publication, or namespaced
  invocation is required. Putting selected third-party skills in a future `jc-misc` plugin is
  a separate ownership decision, not a prerequisite for trying or using them.

Source location and packaging are separate choices. A GitHub marketplace and its local checkout
use the same `jc-plugin install <source> [plugin]` interface. Keep a requested local path local,
quote paths with spaces, and resolve catalog plugin paths from the marketplace root and skill
resources from their owning plugin or skill. A plugin subdirectory without a catalog is not
necessarily an installable marketplace: inspect it and check current CLI behavior. Use the
containing marketplace when available; don't invent a catalog for an instructional question.

## Inventory and removal

`jc-plugin list` reports each plugin's version and enabled state separately for Claude and Codex.
A dash means missing; `(off)` means installed but disabled. Different versions or an installation
in only one tool are not availability in both. `list --all` includes bundled Codex plugins.

For individual skills, use the actual session's skill selector: `/` in Claude Code and `$` or
`/skills` in Codex. Inspect the enabled plugins' manifests and their referenced skill directories
when a file-level inventory is needed. Include standalone project skills at `.claude/skills/`
(Claude) and `.agents/skills/` (Codex), personal skills at `~/.claude/skills/` and
`~/.agents/skills/`, plus any legacy or configured locations exposed by the installed harness.
Check SKILL.md, effective settings, and fresh-session discovery. Automatic visibility is not a
complete inventory: `disable-model-invocation` and Codex `allow_implicit_invocation: false` make
a skill explicit-only, not unavailable. Match discovered commands to manifests and standalone
folders rather than counting every command or just the model's visible skill descriptions.

Claude 2.1.283 exposes callable names in the `slash_commands` field of its fresh-session
`--output-format stream-json --verbose` init event; this also includes built-in commands.
Its [current skill documentation](https://code.claude.com/docs/en/skills#override-skill-visibility-from-settings)
says `skillOverrides` applies to standalone/bundled skills, **not plugin skills**. Manage plugin
availability through plugin enablement. The tested plugin skills remained callable despite
same-named `off` entries, so do not subtract those entries from a plugin's skill count.
Use each harness's current discovery rules; report the scope of an incomplete inventory and
uncertainty when observations disagree. Do not infer who changed settings or when from a
configuration snapshot. Before diagnosing a broken skill, resolve and check the referenced
file itself. A filtered listing that omits scripts or hidden files does not prove they are missing.

There is no universal list of uninstalled skills. Compare a named repository's catalog and
referenced skill paths with observed installations and enabled state. Distinguish a missing
plugin from individual standalone copies. If no source is named, ask which repository or catalog
John wants to compare. For “what skills and uninstalled”, briefly cover installed inventory,
missing skills from a chosen source, and removal instead of guessing one meaning.

For removal instructions, show `jc-plugin uninstall <plugin>` and the verification command.
When asked to do it, run it, then inspect `jc-plugin list` for both tools. Remove only the requested
plugin; its marketplace registration may remain. For standalone skills, remove the requested
copy or link from the discovery location, preserving the source folder and unrelated skills.
