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
| Scale | How large is the resource? | Question/example count; instance count; problems; hours (as reported by the source) | Report the resource's own reported scale metric; don't normalize across resources that use different units. |
| Construction & Grounding | How was the resource — and its reasoning representation — built? | Expert-authored; sourced from textbooks/papers; automatically generated/extracted; human-in-the-loop pipeline; synthetic perturbation | Describes provenance of the data itself; whether that data was later checked is a separate question (see General Validation and Reasoning Human-Checked?). |
| General Validation | What quality-control process was applied to the resource as a whole? | Expert annotation; human-in-the-loop curation; execution-based checks; automated multi-agent verification; expert rubric-based grading | Distinct from Reasoning Human-Checked? and Errors Human-Checked?, which are specific to whether the reasoning trace or error labels (not the resource generally) were checked. |
| Best-Supported Use | What is this resource most defensibly used for, given how it's actually coded? | e.g. "Biomedical answer and explanation generation"; "Multi-hop evidence composition" | A scoped, evidence-backed recommendation — not a claim about every possible downstream use of the resource. |
| Key Limitation | What is the main caveat a reader should know before relying on this resource's reasoning signal? | e.g. partial explanation coverage; unverified provenance; answer-conditioned explanations; normative rather than process-faithful structure | Name the specific limitation found during verification; don't just restate the Supervision Level. |
| Inclusion Status | Does this entry clear the survey's scope bar for explicit scientific reasoning, and how confidently? | Include; Likely include; Borderline; Training resource only | Derived mechanically from Supervision Level, not an independent judgment call — see "Inclusion status is derived from Supervision Level" below for the full rule. |

## Inclusion status is derived from Supervision Level

`Inclusion Status` looks like a separate judgment call per entry, but it's
actually mostly determined by `Supervision Level`:

- **Pure R0** (every item in the resource is final-answer-only — no
  reasoning representation anywhere) → **out of scope, removed from
  `data/inventory.csv` entirely**. The survey characterizes *explicit
  scientific reasoning*; a resource with nothing on that dimension has
  nothing to characterize, so it doesn't get a coded row, even if it's a
  well-known benchmark. See "Excluded: no explicit reasoning" below for the
  record of what was removed and why.
- **Mixed R0/R1+** (some real, verified subset carries an explicit
  reasoning representation, even if most items don't) → stays in the
  inventory as **Borderline** or better (Likely include / Include). A
  partial signal still counts.
- **R1 and above, verified** → **Include** or **Likely include**, per how
  well-verified the representation and its construction/validation are.

Practically: when verifying a Borderline/Low-confidence row, if the
verification lands the entry on *pure* R0, remove it from
`data/inventory.csv` and add it to the excluded list below — don't leave it
in the CSV under a "Historical context only" label and don't treat removal
as a fresh judgment call each time.

A related, differently-motivated category: **Training resource only**
(e.g. MegaScience, TextbookReasoning) — these *do* carry real reasoning
representations (R2/R3) and stay in the inventory; they're just flagged
because they're training data rather than evaluation benchmarks, which is a
different exclusion reason (resource type, not missing reasoning) — don't
remove these the way pure-R0 entries are removed.

## Excluded: no explicit reasoning

These were checked and found to be pure R0 (final-answer-only, nothing on
the survey's central dimension), then removed from `data/inventory.csv`
per the rule above. Kept here — not as coded rows — so the paper can
acknowledge the scope boundary by name (a sentence in intro/related-work,
not a data table) without a reader wondering if a well-known benchmark was
simply overlooked:

- **ARC** (2018) — multiple-choice science QA; final answer only.
- **MedQA** (2020) — multiple-choice medical QA; final answer only.
- **GPQA** (2023) — graduate-level science QA; final answer only.
- **OpenBookQA** (2018) — the per-question fact link exists only in a
  separate file the dataset's own repo calls "Oracle knowledge — a
  hypothetical setting," not the standard train/dev/test split anyone
  evaluates on.
- **TheoremQA** (2023) — public release schema is question/answer/type
  only; no solution or rationale field exists.
- **MaCBench** (2024) — dataset card states explicitly: "questions include
  final answers without rationales."
- **SciTab** (2023) — only the verdict label ships; no evidence-span or
  cell-level annotation is released, despite the task's table-reasoning
  framing.
- **SciEval** (2024) — objective questions (multiple-choice/fill-in-blank/
  judgment) are final-answer-only; the "subjective" experimental-data
  questions are graded manually by the paper's own authors with no
  released rubric, reference answer, or reasoning trace a downstream user
  could access.

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
for full definitions and coding rules: Reasoning Producer, Reasoning Producer
Details, Reasoning Human-Checked?, Reasoning Human-Check Details, Errors
Included?, Error Origin, Error Granularity, Error Labels/Taxonomy, Errors
Human-Checked?, Error Human-Check Details, Evidence Confidence.

`Reasoning Producer`'s recommended values fold "scientist" into `Domain
expert` — both mean someone with genuine subject-matter expertise in the
resource's specific field, whether their day job is research or clinical
practice. Only code `Domain expert` when that field-specific expertise is
actually confirmed (a physicist for a physics benchmark, a clinician for a
clinical one) — a generalist annotator or an expert in an unrelated field
doesn't qualify, and free-text nuance about the producer that doesn't fit
the standardized category (a named source, a sourcing caveat, an
uncertainty) belongs in `Reasoning Producer Details`, not in `Reasoning
Producer` itself.

## Open decision: top-level organization of the README

`data/inventory.csv` is the flat source of truth (53 entries as of writing).
Not yet decided: which dimension the README's public-facing list should be
*sorted by* — candidates are Scientific Domain, Primary Task, or Supervision
Level (R0–R5). Revisit once it's clear which split avoids both single-entry
buckets and one dominant bucket; `data/inventory.csv` has enough entries now
to check this empirically rather than guessing.
