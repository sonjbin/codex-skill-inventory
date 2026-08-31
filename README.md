# Codex Skill Inventory

Reusable personal skills, agent guidance, and experiment workflow templates for Codex.

## Contents

| Path | Purpose |
| --- | --- |
| development/git | Git commit, pull request, and tag workflows |
| development/review | Pull request review workflow |
| development/experiments/experiment-runner | Reproducible training and evaluation experiment workflow |
| documentation | Documentation writing guidance |
| docs/experiments | Experiment guide, state template, index, and experiment template |
| AGENTS.md | Repository-level Codex operating rules |

## Use

Copy or link an individual skill directory into the Codex skills directory.

For example:

    C:\Users\<user>\.codex\skills\development\experiments\experiment-runner

Use the experiment documents in a project that runs repeated training or evaluation work. Keep project-specific state, logs, artifacts, and automation in that project; this repository stores the reusable workflow only.

## Experiment workflow

1. Read the experiment guide and current state.
2. Define one hypothesis and one primary change from the baseline.
3. Run and track the experiment with compact status rather than repeated raw-log reads.
4. Record the result, comparison, decision, artifacts, and next action.

Create log parsing or status scripts only after examining the target project's actual training code and representative logs.

## Validation

- Each skill contains a SKILL.md file with discovery metadata and operating instructions.
- Experiment documents provide completion conditions and validation methods.
- No project-specific training code, logs, datasets, or model artifacts are included.
