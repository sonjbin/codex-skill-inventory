---
name: experiment-runner
description: Run and track reproducible training or evaluation experiments with topic indexes, shared environment profiles, compact status, and baseline comparisons. Use for repeated ML experiments; not a one-off command without an experiment record.
---

# Experiment Runner

## Locate and classify

1. Find the management root declared in workspace/repository AGENTS.md. A recommended layout is `<workspace>/experiment-management/`; use the declared root rather than assuming a workstation path or repository-local `docs/experiments`. All workflow paths below are relative to that root.
2. Read `experiments/INDEX.md`, then only the relevant topic index and required reports. For execution, also read `experiments/EXPERIMENT_GUIDE.md`, compact `experiments/CURRENT_STATE.md`, and the applicable section of `ENVIRONMENT.md`.
3. Before creating files, identify the owning topic and existing baseline in the action plan. Same-study reruns get a new run ID; related comparisons become studies under the existing topic; only an unrelated objective gets a new topic.
4. Use `experiments/templates/EXPERIMENT.md`. Reserve a unique study ID after checking all topic indexes; serialize shared index writes. Keep one owner for cross-topic results and link from other topics.

Do not load all reports, archived state, or raw logs to discover experiments. Do not invent commands, dataset locations, metric schemas, or completion signals when documentation/code do not establish them.

## Configure and execute

- Resolve shared defaults → model/task profile → scoped exception → explicit run overrides. Keep defaults and reusable/one-off exceptions in ENVIRONMENT.md with scope, reason, evidence and revision.
- A historical exception is not a future default. Verify resource availability and actual command/config before launch; documentation alone does not apply settings.
- Report the profile and differences; preserve the complete resolved configuration, profile revision/hash, actual versions/GPU placement, seed and command in the run manifest.
- Capture every participating repository commit and dirty patch/hash, input/prompt/model/checkpoint hashes, metric version/normalization/aggregation, and baseline lineage. Mark missing historical provenance unknown rather than reconstructing it from current settings.
- Keep code and large artifacts in the owning repository's unique run path. Link workspace-relative paths and hashes from the central study. Never overwrite another run or checkpoint.
- Follow the project smoke policy. Delegate only bounded independent work with explicit output ownership; no concurrent writes to a shared working tree/output.

## Track and finish

- Inspect compact status (state, progress, error counts, updated_at) at milestones; read relevant raw log sections only on anomalies or stalled updates.
- After the same failure recurs following one targeted correction, stop retries and record evidence and next diagnosis.
- Record results, baseline delta, interpretation, decision, validation/limitations and artifact paths. Distinguish superseded results and incompatible dataset/marker/metric conditions.
- Update the topic index; update the global index only for topic changes. Keep CURRENT_STATE.md to active/blocked work and next actions, within 60 lines; put completed history in studies.
- Return a compact outcome with links. Check cardinality/hash/metric reproduction and cleanup as required by the actual experiment.

## Human-readable reporting

When a reader-facing report is requested, hand the verified study, baseline, metric sources, denominators, comparison conditions and unresolved validation issues to the research-report skill. Preserve the study and run artifacts. Use its quality rubric before delivering a Markdown report or presentation summary.

## Automation

Create deterministic status/summarization scripts only after inspecting the real entrypoint and representative normal/failure artifacts. Document inputs, schema, command, missing-field behavior, completion/failure signals and validation cases. Never assume a generic framework log format.
