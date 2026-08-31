---
name: experiment-runner
description: Run and track reproducible training or evaluation experiments with compact state, baseline comparison, and documented decisions. Use for repeated ML or model experiments; not for a one-off command with no experiment record.
---

# Experiment Runner

Use this skill to operate a project experiment workflow without accumulating raw logs in the main agent context.

## Start

1. Read the project experiment guide and current state. In this inventory, use docs/experiments/EXPERIMENT_GUIDE.md and docs/experiments/CURRENT_STATE.md.
2. Confirm the experiment objective, baseline, one main change, validation criteria, stopping condition, output path, and resource availability.
3. Create an experiment record from docs/experiments/templates/EXPERIMENT.md; assign the next available E### ID and register it in EXPERIMENT_INDEX.md.

Do not infer the training command, metric schema, log format, dataset location, or completion marker. Ask for direction when the project documentation and runnable code do not establish them.

## Execute

- Keep each experiment independently reproducible: record commit, dataset version, seed, model/checkpoint, command, resources, and output path.
- Do not reuse an output directory or overwrite a checkpoint belonging to another run.
- Delegate only a bounded, independent experiment or analysis to a subagent. Give the worker the experiment record and an explicit output ownership boundary.
- Do not repeatedly poll full raw logs. Prefer a compact status artifact; otherwise inspect only scheduled milestones or anomalies.

## Track and diagnose

Inspect detailed logs only for divergence, NaN/Inf, OOM, process failure, metric collapse, unexpected exit, or stalled status updates.

After the same failure recurs following one targeted correction, stop retrying. Record the evidence and choose root-cause analysis or a different approach.

## Finish

1. Record key metrics and compare them with the baseline.
2. Write the interpretation, decision (ACCEPT, REJECT, INCONCLUSIVE, or FAILED), next action, and artifact paths in the experiment record.
3. Update CURRENT_STATE.md and EXPERIMENT_INDEX.md.
4. Return a compact summary containing status, main change, key results, baseline comparison, recommendation, and artifact paths.

## Project-specific automation

Create a status or summarization script only after inspecting the real training entrypoint and representative normal and failure logs.

Document the script input format, output schema, invocation command, missing-field behavior, completion/failure signals, and validation cases. Keep its output limited to the fields needed for experiment decisions. Do not include a generic parser that assumes a particular framework or log format.
