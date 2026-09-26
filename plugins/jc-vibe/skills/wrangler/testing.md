# Testing a skill in Claude Code and Codex

Testing covers both tools in John's workflow. A request to perform a test means run it where
feasible, not just describe a plan. Check local `claude --help`, `codex exec --help`, and current
[Claude skill docs](https://code.claude.com/docs/en/skills) and
[Codex skill docs](https://learn.chatgpt.com/docs/build-skills) before relying on options or discovery.
The project layouts below were exercised with Claude Code 2.1.283 and Codex 0.157.1.

## Ordinary skill folder, no plugin

Create a temporary project with two discovery directories. Copy or link the **whole** candidate
folder, including relative scripts and resources:

```text
scratch/
  .claude/skills/<name>/SKILL.md   # Claude: /<name>
  .agents/skills/<name>/SKILL.md   # Codex: $<name>
```

Both entries may be symlinks to the same absolute candidate directory. Initialize a temporary
Git repository, start both tools from its root, and give each a separate output path. This does
not require a marketplace, a plugin manifest, a plugin version, or a GitHub push. Personal
installation uses `~/.claude/skills/<name>/` and `~/.agents/skills/<name>/` instead; do not overwrite
an existing skill without checking its identity. For a remote source, fetch the repository and
copy the selected complete skill folder, recording the commit.

Close standard input for noninteractive child processes so an inherited shell pipe cannot leave
them waiting for additional input. Start fresh actual harness processes. For example, from scratch, using the candidate's real name:

```sh
claude -p '/<name> <realistic task>' --output-format stream-json --verbose </dev/null
codex -a never exec --json -s workspace-write '$<name> <realistic task>' </dev/null
```

Read current CLI help before launching these commands. The tested Codex 0.157.1 supports
`-s workspace-write`; it does not advertise the older `--full-auto` flag. Use the actual installed
options rather than an option remembered from another version.

Check permission settings so required file reads and benign actions can run; a denied tool call
is a blocker to that check. Do not change the user's global permission settings for a test.
Use supported project isolation, record any real installation changes, and restore only test-created
state. Keep expected answers and evaluator instructions outside the tested session's context.

## What counts as evidence

Choose a realistic task and expected observable outcome before running it. A small fixture can
write a file using a relative resource, giving an exact result to check. Exercise the actual skill
on a representative task too; a dummy fixture proves loading mechanics, not that skill's quality.

Record separately:
- Structure: valid SKILL.md and required resources exist.
- Discovery/loading: a fresh session finds and invokes the intended skill, with the loaded path
  or content identity visible in the transcript. A plausible answer alone is insufficient.
- Behavior: inspect the produced artifact or action against the expected outcome.
- Integration: actual install/update/removal results and subsequent skill invocation in each tool.

Use independent fresh sessions for independent prompts and a continued session for follow-ups.
Try an ordinary paraphrase, and a missing-resource or command failure: expect honest failure,
not invented output. Keep prompt, transcript, tool results, CLI versions, candidate identity,
pass/fail/blocker, and cleanup result. Copy transcripts and checked outputs to a durable evidence
folder before deleting scratch projects; cleanup should not erase the proof. Report partial
success accurately. Remove temporary links
and generated test state when finished, leaving the candidate source intact.

## Plugins and stale copies

For a packaged candidate, inspect catalogs and manifests, install the selected plugin using
`jc-plugin install <marketplace-root> [plugin]`, and verify both tool states. Local roots work
without publishing; use the marketplace root, not an assumed bare plugin path. Claude also has
session-local `--plugin-dir`, but that alone is not a Codex test or a cross-tool install test.
Preserve existing marketplace source registrations and unrelated installations.

For a released plugin, compare `jc-plugin list`, installed manifest versions, and loaded file
content with the source commit. Follow the source repository's release process and run
`jc-plugin update <plugin>` when appropriate, then launch fresh sessions in both tools.

For standalone candidates, compare resolved paths and file hashes, including resources. Refresh
copies or repair links to the actual candidate; there is no plugin version to bump. A distinct
content marker and changed expected artifact can prove that the new content ran. Do not remove
an unrelated installed plugin merely to avoid a name collision: use an isolated project and
confirm which path loaded. An already-open session is not evidence of a refreshed candidate.
