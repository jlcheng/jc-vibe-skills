# jc-vibe-skills

A Claude Code and Codex plugin marketplace. One experimental plugin so far, `jc-vibe`, holding skills that have not yet met the bar for `jc-agent-skills`.

## Adding or changing a skill

Every skill change ships as a `jc-vibe` plugin version bump. Do all of these, in order:

1. **Bump `plugins/jc-vibe/.claude-plugin/plugin.json` and `plugins/jc-vibe/.codex-plugin/plugin.json` to the same version.** A new skill or capability is a minor bump; a fix is a patch bump. Update the description in both to list each skill, and keep the Codex `interface.longDescription` in sync.
2. **Update `.claude-plugin/marketplace.json`.** Keep its `jc-vibe` description concise and accurate. Both it and `.agents/plugins/marketplace.json` must point `jc-vibe` at `./plugins/jc-vibe`.
3. **Add a `## Change Log` entry in `README.md`.** Put the newest version first and describe the user-visible change.
4. **Update the Plugins table and Layout block in `README.md`.**
5. **Update `EXPERIMENTS.md`.** Record test coverage, limitations, commands, network behavior, and promotion readiness.

Skills may have their own `version` in `SKILL.md`; that is separate from the plugin version.

Do not promote a skill to `jc-agent-skills` without testing and review.
