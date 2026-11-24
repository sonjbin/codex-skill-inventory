# Codex Skill Inventory

Reusable personal skills, agent guidance, and experiment workflow templates for Codex.

## Contents

| Path | Purpose |
| --- | --- |
| development/git | Git commit, pull request, and tag workflows |
| development/review | Pull request review workflow |
| development/experiments/experiment-runner | Reproducible training and evaluation experiment workflow |
| [documentation](documentation/documentation/SKILL.md) | Technical documentation for code, APIs and pipelines |
| [research-report](documentation/research-report/SKILL.md) | Reader-facing experiment reports, comparisons and presentation summaries |
| docs/experiments | Workspace topic indexes, compact state, guide, and study template |
| docs/ENVIRONMENT.md | Shared environment profiles and scoped exceptions template |
| AGENTS.md | Repository-level Codex operating rules |

## Use

Keep this repository as the source of truth and symlink each managed skill directory into the skill discovery location used by your Codex installation. Editing the repository then updates the installed files without a second copy step.

The current official user discovery location is `~/.agents/skills/`; Codex supports symlinked skill folders. This workspace currently exposes skills through `.codex/skills/`, so verify the active installation location before switching it. See [official skill documentation](https://learn.chatgpt.com/docs/build-skills).

For an installation already using `.codex/skills`, the intended relationship is:

```text
.codex/skills/development/experiments/experiment-runner
  -> codex-skill-inventory/development/experiments/experiment-runner
```

Before replacing an existing copy, compare its contents with the repository and preserve local-only edits. Move the old copy outside scanned skill directories, then create the link and verify skill discovery. Avoid exposing the same skill through multiple discovery roots.

Link only managed skill folders. Keep Codex runtime configuration, authentication, session data, bundled system skills and plugin caches outside this repository. Workspace experiment documents are project-owned copies of templates, not live links back to inventory templates. Global AGENTS rules can be linked separately only when their intended scope and contents match; repository-specific AGENTS remain local.

Copy the contents of `docs/` into `<workspace>/experiment-management/`. Declare this root in workspace AGENTS.md and link it from participating repository AGENTS.md. Keep this management directory under its own Git history; retain code, logs, predictions and checkpoints in the owning repositories. This inventory stores reusable templates only.

For research reporting, link the entire `documentation/research-report/` folder as `research-report` under the active skill root so the examples and rubric resolve. Check the link target and confirm the skill appears in a fresh session. For existing workspaces, merge the document routing from `AGENTS.md` and the reporting section from `EXPERIMENT_GUIDE.md` into their project-owned copies, preserving local rules and study records.

## Experiment workflow

1. Search the global topic index, then only the relevant topic index and required report.
2. Reuse an existing study for reruns, add related studies under its topic, and create a new topic only for an unrelated objective.
3. Read shared environment profiles and compact active state for execution. Register scoped exceptions; preserve resolved run settings and all participating repository revisions.
4. Track compact status; inspect raw logs only for anomalies.
5. Update the study and topic index with results, baseline comparison, decision and artifacts. Keep completed history out of current state.
6. When a reader-facing report is requested, use research-report with the verified study and metric sources.

Create project-specific status scripts only after inspecting actual normal and failure artifacts. With linked installation, edit the repository copy only; until linked, verify installed and inventory experiment-runner copies match.

## Validation

Use the [research report comparison cases](evaluation/research-report.md) to evaluate report quality under controlled skill, example and review conditions.

- Each skill contains a SKILL.md file with discovery metadata and operating instructions.
- Experiment documents provide completion conditions and validation methods.
- No project-specific training code, logs, datasets, or model artifacts are included.
