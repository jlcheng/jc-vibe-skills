# Experiments

This is the record for skills in `jc-vibe`. 
For each skill, record:

- What it does and where it came from.
- What commands it runs and what it sends over the network.
- What has and has not been tested.
- Known limitations, failure modes, and the date it was last checked.
- Whether it is ready to promote to `jc-agent-skills`.

## wrangler

### Initial assessment (historical, 0.3.0)

- **What it does:** Guides John through his skill workflow: which of his three places a skill
  belongs in (vibe, published, someone else's repo), and the `jc-plugin` commands to install,
  update, remove, and list plugins in Claude Code and Codex. Written by John and Claude on
  2026-09-26.
- **Invocation:** By name only (`/jc-vibe:wrangler`, `$jc-vibe:wrangler`); neither tool starts it on its own.
- **Commands and network:** The skill itself runs nothing. It suggests `jc-plugin`, `claude plugin`,
  `codex plugin`, and `git` commands, which fetch from GitHub when run.
- **Tested:** Installed through `jc-plugin` into both tools; a fresh session in each loaded it
  (2026-09-26).
- **Compatibility checked (2026-09-26):** Codex CLI 0.157.1 installed
  `mattpocock-skills@mattpocock` 1.2.3 from its Claude catalog and manifest. Individual skills
  were not executed.
- **jc-plugin checked (2026-09-26):** John's terminal output confirms that
  `jc-plugin install https://github.com/mattpocock/skills` installed version 1.2.3 in both
  tools, and `jc-plugin uninstall mattpocock-skills` removed it from both. This supersedes
  the earlier claim that `jc-plugin` required both catalogs.
- **Not tested:** Whether its advice holds up across a real promotion from vibe to published.
- **Limitations:** Local testing before pushing is not covered yet. The `jc-misc` plugin it recommends for copied
  skills doesn't exist yet.
- **0.3.0:** The workflow moved into `workflow.md`, written as John's own plan. The skill checks
  other people's repos itself.
- **Ready to promote:** No.

## Wrangler 0.4.0 verification in progress (2026-09-26)

Evidence directory: `/Users/jcheng/Downloads/wrangler-evidence/`, evaluator status in `STATUS.md`.
The original handoff is `/Users/jcheng/Downloads/handoff.txt`.

- Baseline on 0.3.2: actual fresh Claude Code 2.1.283 and Codex 0.157.1 sessions for installation
  advice, inventory, placement, testing advice, and standalone advice. Both tools omitted the
  other harness in testing advice; inventory guidance was incomplete. Raw transcripts retained.
- Harness mechanics: a standalone fixture with a relative JSON resource and Python script loaded
  through project `.claude/skills` and `.agents/skills` links; both produced the exact receipt.
  These fixture results establish standalone mechanics, not final Wrangler acceptance.
- Commands: `claude -p` with JSON event output, `codex exec --json`, `jc-plugin list`, local
  Python fixture script. Documentation and named public repositories are fetched over HTTPS;
  actual harness prompts use the configured model services. No secrets belong in evidence.
- 0.4.0 adds explicit cross-tool behavior testing and removes required jc-misc packaging for
  standalone usage. Existing historical claims above are not proof of 0.4.0 behavior.
- Outstanding: full final-candidate prompt matrix, real source/packaging action cells, state and
  failure variations, held-back paraphrases, cleanup checks, and independent evidence review.
  No claim of completion or promotion readiness. Not ready to promote.

### 0.4.1 decision correction

Independent review of 0.4.0 evidence found that both tools skipped the unresolved placement
question, and Codex offered multi-plugin commands without asking which plugin was intended.
0.4.1 clarifies these two decisions. Final-candidate acceptance remains in progress.

Further 0.4.0 evidence: actual Matt Pocock installation and removal in both tools via both
harnesses, plus harmless skill invocation in fresh Claude and Codex sessions. Claude's Humanizer
action inspected the full GitHub repository, copied complete standalone files into both project
discovery locations, and exercised both actual harnesses. Separate fact-preservation behavior
checks and final-candidate reruns are recorded in the evidence directory. A Claude standalone
test initially hit runner permission denials; it was retained as blocked and retried with a
session-only permission configuration for the authorized temporary workspace.

### 0.4.2 completion of installation checks

Review of 0.4.1 found that installation action sessions stopped at state/content checks for local
and dual-catalog plugins, leaving fresh-session behavior to the evaluator. Inventory also treated
some individually disabled skills as available. 0.4.2 corrects both behaviors and avoids assuming
Wrangler is the candidate in generic testing advice. Final acceptance is still unproven.

Supporting jc-plugin changes are published in privmono at a074bfd. Meaningful failing regression
tests preceded the GitHub-source equivalence fix; 25 tests, clippy and formatting pass. The built
~/bin/jc-plugin succeeds against real tools for shorthand with an existing HTTPS registration.
The earlier Claude-catalog fallback is published at a327a7c, with parent-failure evidence retained.
A transient Claude quota response was rechecked: later fresh sessions succeeded, so it is not
currently classified as a persistent external blocker.

### 0.4.3 discovery and test-run corrections

0.4.2 tests exposed confusion between automatic visibility and callable skills. Current Claude
skill documentation explicitly excludes plugin skills from `skillOverrides`; fresh init command
catalogs and successful explicit invocations confirmed that behavior in 2.1.283. Earlier test
responses subtracting nine same-named override entries from Matt's plugin were incorrect.
No existing overrides were edited. 0.4.3 clarifies the scope and avoids inferred change history.

Two Claude test orchestrations tried the retired Codex `--full-auto` flag before recovering.
The supported `-s workspace-write` example now appears directly in testing.md, with a reminder
to consult current help. Tests must preserve logs/artifacts before cleaning temporary discovery
state. Final 0.4.3 acceptance remains to be run; successful 0.4.2 actions are not presented as
proof of this candidate.

### 0.4.4 installation guidance correction

A real Claude 0.4.3 session using a simulated one-tool-only inventory recommended an installed `plugin@marketplace` identifier as an install source. The workflow now distinguishes source arguments from installed identities, with the supported source-plus-plugin example. Repository inspection now explicitly covers complete manifests and resolved referenced paths; partial manifest reads had left gaps in guidance evidence. Final 0.4.4 acceptance remains pending.

Two Claude-orchestrated 0.4.3 Codex children stalled before starting a session, with stderr `Reading additional input from stdin...`. The noninteractive examples now close stdin explicitly. These stalls are retained as failed checks, not skill behavior passes.

### 0.4.5 inventory evidence correction

A real Claude 0.4.4 session in the simulated version-mismatch workspace falsely diagnosed a missing Python script from a listing filtered to SKILL.md and JSON. The script was present in both copies throughout the test. Guidance now requires directly checking a referenced path before declaring it absent. The failure is retained; final0.4.5 acceptance remains pending.

### 0.4.5 acceptance snapshot

The complete final-candidate run recorded 94 case/harness outcomes against skill release
`89a367b`: 66 PASS and 28 BLOCKED by Claude's reported usage/spend limit. This is not complete
acceptance or promotion readiness. Claude Code 2.1.283 and Codex CLI 0.157.1 were actually
invoked; the evaluator document/rubrics were kept out of tested-agent contexts. Guidance,
held-back paraphrases, simulated state/failure fixtures, actual standalone receipt behavior,
remote/local plugin operations, stale copies and Humanizer are represented separately.

Both native plugin installations and Codex behavior succeeded for remote Claude-only and
remote dual-catalog sources, and for local copies including a path with spaces and a relative
path. Final Claude behavior repetitions remain unproven where quota interrupted them.
Both P20 Humanizer installations and smoke tests succeeded before the limit; subsequent
Claude rubric probes were blocked. Earlier Humanizer Claude rewrites invented meaning, and
one final Codex rewrite has malformed CriticMarkup. Third-party quality is not claimed to
pass universally. Validator compatibility limitations and incidental response caveats are
recorded rather than omitted.

Evidence and per-case prompts, commands, identities, setup, transcripts, timestamps and grades:
`/Users/jcheng/Downloads/wrangler-evidence/REPORT.md` and `CASE-MATRIX.md`. Independent review
found no material Wrangler failure in completed final cases. Global test plugin state was
restored: marketplace snapshots exactly match the pre-action snapshots, unrelated plugin
records are unchanged, and existing jc-code 1.6.1 is preserved. Scratch fixtures are retained
for targeted retries of blocked cases. No HOME/CODEX_HOME override or global permission
change was used. The user reported purchasing credits; subsequent availability checks still
reported the monthly limit. Billing settings were not changed. The skill candidate remains
0.4.5 for those retries; this entry only updates the evidence record.

### 0.4.6 installation action corrections

After Claude capacity returned, 0.4.5 retries exposed two action failures: Claude P2 read
the catalog and manifest but skipped checking referenced paths before installing; Claude P17
only verified an existing installation instead of executing the explicit install request.
Successful loading did not satisfy these separate requirements. The retained retry grades
record both failures. Guidance now applies preflight explicitly to actions and uses the
supported install operation for an already-listed plugin without destructive reset.

Both Humanizer rubric probes executed after capacity returned. One Claude rewrite invented
routing details and personal uncertainty; the other preserved the rubric facts. A receipt
fixture also mishandled a relative output path in one Claude child, which Wrangler exposed
and reported. These skill behavior failures remain distinct from competent testing.

0.4.6 requires a complete fresh acceptance run. No completion or promotion readiness is claimed.
The supporting jc-plugin source and binary are unchanged. Source/installed identities, original
failures, subsequent retries and independent grades remain in the evidence directory above.

### 0.4.7 intent, scope and inventory corrections

The 0.4.6 run exposed Claude failures to honor a selected vibe home and project installation
scope, distinguish absent plugins from absent individual skills, check current state for a
multi-plugin question, and use the current Codex standalone location. Its accidental personal
Humanizer files were proven absent before the test, archived with hashes, then removed.
No unsupported success is inferred from these attempts; remaining cases were stopped.
Guidance now leads with settled user decisions, makes standalone scope/whole-folder handling
explicit, and states the inventory distinctions at the entrypoint.

Native session records also reveal model drift: prior Claude acceptance sessions used
`claude-opus-5-5`; 0.4.6 defaulted to `claude-sonnet-5`. Subsequent outer Claude sessions will
explicitly select the recorded Opus baseline with the supported `--model` flag. This controls
a changed test condition, not a claim that Sonnet passed. Both models' results are retained;
conclusions apply to actual recorded models and harnesses, not every possible model.
Nested behavior tests remain real Claude Code/Codex runs with their own recorded identities.

0.4.7 has not yet passed full acceptance. No promotion is authorized or claimed.

### 0.4.8 ownership, recovery and evidence corrections

The 0.4.7 run completed70 records:44PASS,21BLOCKED by Claude's recurring monthly-spend
response,5FAIL;24 further cases were stopped, not passed. Both harnesses defaulted unresolved
ownership to vibe, and Codex repeated it on the held-back placement prompt. The entrypoint
now explicitly asks John for an unresolved home, distinguishing that from a stated uncertainty
or an already chosen home. A Claude simulated-version recovery also used an installed
`plugin@marketplace` identity as an install source; the supported source/identity distinction
and version-refresh operation now appear together in the entrypoint.

Claude P20 successfully installed and loaded complete project copies but overwrote older files
at a fixed temporary evidence path. Earlier outer/native session logs preserve substantive
proof; this does not restore the original stdout bytes or reverse the failure. Testing guidance
now calls for unique scratch/evidence directories. All known failures and recovered proof are
retained under candidate-0.4.7 and its independent review. Global plugin state is preserved.

Fresh explicit Opus and Sonnet availability requests both returned the spend-limit response.
No billing, account, model-default or permission settings were changed.0.4.8 full acceptance
is unproven; focused checks will precede another complete run when Claude capacity permits.

### 0.4.8 verification snapshot

Independent review passes 31 Codex guidance, inventory/state and placement-follow-up cases
on `68cb404` with Codex CLI 0.157.1 and actual model `gpt-6-astra`. Simulated inventories
remain labeled; these are not 31 installation integrations. Both installed skill folders match
the released source. The remaining 63 acceptance cells are unproven on this candidate.

Fresh Claude Opus and Sonnet availability checks, including another after the Codex work,
returned the monthly-spend-limit error. This is an observed service response, not proof of the
actual account balance or spending cap. No billing or account settings were changed.
The independent preservation audit passes for global marketplace/plugin state except the
authorized Wrangler upgrade. Existing jc-code is unchanged. Fixtures and evidence are retained
for pending cross-tool checks; acceptance and promotion readiness are still not established.

Current evidence: `/Users/jcheng/Downloads/wrangler-evidence/REPORT.md`, `CASE-MATRIX.md`,
`candidate-0.4.8/case-index.json` and `review-0.4.8.md`. Earlier failed attempts remain intact.

### 0.4.9 plugin invocation identity correction

John revised verification to Codex only and requested low-cost models. New outer and nested
behavior checks use gpt-6-luna; no further Claude model tests or health probes are run.
Native plugin installation/listing still checks both registries. The prior Astra checks and
historical Claude results retain their original scope and are not relabeled as Luna coverage.

The 0.4.8 Codex stale-plugin test refreshed the right cache and demonstrated changed behavior,
but its final guidance confused a different plugin's qualified invocation with a loading failure
and recommended an ambiguous short name. Direct checks prove both original and test plugin
namespaces work and select their respective content. Testing guidance now ties qualification to
the actual installed plugin manifest, rather than the source directory or a duplicate short name.
Evidence and independent review: /Users/jcheng/Downloads/wrangler-evidence/,
candidate-0.4.8-codex-only and review-0.4.8-codex-only.md. Receipt fixture response omissions
and missing-output-parent failures were detected and reported; they are target-skill failures,
not false claims of successful behavior. Test-created global plugins were removed and original
marketplace registrations restored. No Claude behavior is claimed under the revised scope.

0.4.9 verification is pending. No complete acceptance or promotion readiness is claimed.

### 0.4.10 question intent and unresolved identity

Fresh Codex Luna verification passes the 0.4.9 namespace regression but demonstrates three
other decision failures: a multi-plugin question receives all install commands before a choice;
an unnamed draft is assumed to be Wrangler and placed accordingly; and a feasibility question
about a bare plugin directory triggers an actual install, including replacing an existing plugin
source. The latter used a full-access test harness, unlike earlier read-only guidance sessions,
which exposed the mutation. Its native source registration and installation were restored to the
original GitHub source/version, with commands preserved. Remaining global action cases were
stopped after these failures rather than spending on a known failing candidate.

The entrypoint now leads with question versus action intent and keeps the managed candidate's
identity separate from Wrangler. Multi-plugin selection remains unresolved until John chooses;
the workflow's placement description no longer suggests an automatic initial home. These are
corrections supported by real failed sessions, not a claim of new behavioral verification.
Evidence: candidate-0.4.9-codex-only and review-0.4.9-codex-only under the existing evidence root.
0.4.10 verification is pending; Claude model testing remains excluded by John.

### 0.4.11 placement is a preference, not a maturity judgment

The three focused 0.4.10 Luna checks corrected the feasibility-question mutation and asked for
multi-plugin selection. Placement still recommended vibe because the unspecified skill was a
draft. The source now explains why that inference is invalid: John chooses a home case by case,
so the next step is his preference, not inspecting draft maturity to decide for him. An explicitly
unsure answer still leads to vibe, and an already chosen home remains settled. Broader0.4.10
tests were not started after the focused failure.0.4.11 behavioral verification is pending.
