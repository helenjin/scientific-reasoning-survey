# Taxonomy

This documents the coding scheme used to annotate every entry in
[`data/inventory.csv`](data/inventory.csv). It is a taxonomy **proposed for
this survey**, not an established literature standard — it should read as
"here is how we coded things," not as a claim that these categories are
canonical.

Machine-readable source of truth for everything below lives in `data/`:
[`coding_dimensions.csv`](data/coding_dimensions.csv),
[`reasoning_representation_levels.csv`](data/reasoning_representation_levels.csv),
[`task_taxonomy.csv`](data/task_taxonomy.csv) (+
[`task_taxonomy_sources.csv`](data/task_taxonomy_sources.csv)), and
[`reasoning_error_guide.csv`](data/reasoning_error_guide.csv). This file is a
human-readable rendering of those.

## Reasoning representation levels (R0–R5)

The survey's central analytic dimension: what explicit form of reasoning a
resource exposes, independent of scientific domain or task.

| Level | Definition | Typical signals | Examples | Note |
|---|---|---|---|---|
| R0 | Final answer, label, score, or outcome only | Multiple-choice answer; numerical result; verdict | ARC; GPQA | May test reasoning without exposing the process. |
| R1 | Supporting evidence or relevant facts without an explicit inference trace | Evidence spans; cited sentences; supporting facts | SciFact; Qasper evidence | Evidence is not automatically an explanation. |
| R2 | Free-text explanation, rationale, worked solution, or derivation | Rationale; ideal answer; worked solution | ScienceQA; MedExQA | A correct explanation may be post hoc or unfaithful. |
| R3 | Structured reasoning representation | Entailment tree; explanation graph; argument structure | WorldTree; EntailmentBank | Structure may be normative rather than process-faithful. |
| R4 | Executable, interactive, or workflow-level process supervision | Code; tool calls; actions; intermediate states | ScienceAgentBench; SciCode | Execution success does not guarantee scientific validity. |
| R5 | Error-, critique-, alternative-, correction-, or revision-aware supervision | Incorrect steps; critiques; repairs; revised hypotheses | eQASC-Perturbed; ProjectionBench | A distinct meta-reasoning signal, not a universal quality ranking. |

## Coding dimensions

Per-entry fields coded in `data/inventory.csv`, beyond the R0–R5 level:

| Dimension | Question it answers | Suggested values | Distinction to watch for |
|---|---|---|---|
| Primary Task | What scientific operation is the model expected to complete? | QA; claim verification; paper comprehension; explanation/proof generation; data analysis; hypothesis discovery/verification; workflow execution | Task describes the objective and expected output. |
| Secondary Task / Variant | What narrower operation or variant is involved? | Evidence retrieval; diagnosis; equation discovery; hypothesis ranking; error detection | Use for specificity without proliferating primary categories. |
| Scientific Domain | Where is the task situated? | Medicine; biology; chemistry; physics; materials science; multidisciplinary | Domain is not a task. |
| Modality | What forms of information are provided or produced? | Text; image; table; code; graph; molecular structure; mixed | Multimodality is not a task. |
| Interaction Setting | How does the system act while solving the task? | Static; staged; executable; tool-using; agentic; interactive | Agenticity is a solution setting, not the scientific objective. |
| Resource Type | What kind of resource is this? | Evaluation benchmark; training dataset; benchmark suite; repository/meta-dataset | Training resources and repositories are not tasks. |
| Reasoning Capability | What kind of inference is required? | Deduction; induction; abduction; causal; mechanistic; quantitative; statistical | Capability and task may cut across one another. |
| Reasoning Representation | What explicit form of reasoning is exposed? | Evidence; rationale; worked solution; entailment tree; graph; code; workflow; critique; revision | The survey's central analytic dimension (see R0–R5 above). |
| Supervision Level | How much explicit process information is available? | R0–R5 | A proposed analytical abstraction, not an established standard. |

## Task taxonomy

Working definitions for `Primary Task` values — see
[`task_taxonomy.csv`](data/task_taxonomy.csv) for the full table (working
definition, typical input/output, literature grounding, and the
boundary/coding rule used to disambiguate each task from its neighbors):
Question answering, Claim verification, Paper comprehension, Explanation or
proof generation, Data analysis, Hypothesis discovery or verification,
Scientific coding or workflow execution, Repository/infrastructure.

## Reasoning-error fields

Per-entry fields used when a resource includes incorrect reasoning, critiques,
or corrections — see [`reasoning_error_guide.csv`](data/reasoning_error_guide.csv)
for full definitions and coding rules: Reasoning Producer, Reasoning
Human-Checked?, Reasoning Human-Check Details, Errors Included?, Error
Origin, Error Granularity, Error Labels/Taxonomy, Errors Human-Checked?,
Evidence Confidence.

## Open decision: top-level organization of the README

`data/inventory.csv` is the flat source of truth (61 entries as of writing).
Not yet decided: which dimension the README's public-facing list should be
*sorted by* — candidates are Scientific Domain, Primary Task, or Supervision
Level (R0–R5). Revisit once it's clear which split avoids both single-entry
buckets and one dominant bucket; `data/inventory.csv` has enough entries now
to check this empirically rather than guessing.
