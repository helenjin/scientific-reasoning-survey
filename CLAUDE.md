# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

This is the data/documentation repo accompanying a survey paper ("A Survey
of Datasets and Benchmarks for Explicit Scientific Reasoning"). There is no
application code — the deliverable is a curated, coded inventory of
datasets/benchmarks plus the taxonomy used to code them. Almost all work
here is editing CSVs and Markdown, not writing software.

## Repo structure

- `data/inventory.csv` — the flat source of truth: one row per included
  dataset/benchmark, coded across ~28 columns (task, domain, modality,
  reasoning representation, construction, validation, error-annotation
  fields, etc.). Currently 53 entries.
- `data/coding_dimensions.csv`, `data/reasoning_representation_levels.csv`,
  `data/reasoning_capability_types.csv`, `data/task_taxonomy.csv` +
  `data/task_taxonomy_sources.csv`, `data/reasoning_error_guide.csv`,
  `data/excluded_resources.csv` — machine-readable definitions backing
  `TAXONOMY.md`. `TAXONOMY.md` is a human-readable rendering of these; if
  you edit the taxonomy, keep both in sync.
- `data/new_resources_added.csv` — running log of resources added beyond
  the original inventory pass. `data/excluded_resources.csv` is its
  counterpart: one row per resource removed from `inventory.csv` under
  the pure-R0 exclusion rule, with the reason and source link.
- `data/scientific_reasoning_resources_expanded.xlsx` — the original
  working spreadsheet these CSVs were generated from. Gitignored (`data/*.xlsx`
  in `.gitignore`) — treat it as a local-only source artifact, not something
  to commit.
- `scripts/xlsx_to_csv.py` — one-off converter from that xlsx into the
  per-sheet CSVs above. Run via `python3 scripts/xlsx_to_csv.py` from repo
  root if the xlsx is regenerated; it's not part of a regular workflow
  otherwise since the CSVs (not the xlsx) are the tracked source of truth.
- `README.md`, `CONTRIBUTING.md`, `TAXONOMY.md` — the only prose docs.

## The central concept: R0–R5 reasoning representation levels

The survey's core analytic dimension is *what explicit form of reasoning a
resource exposes*, independent of scientific domain or task:

| Level | Meaning |
|---|---|
| R0 | Final answer/label/score only — no reasoning process exposed |
| R1 | Evidence/supporting facts, no explicit inference trace |
| R2 | Free-text explanation, rationale, or worked solution |
| R3 | Structured reasoning representation (entailment tree, argument graph) |
| R4 | Executable/interactive/workflow-level process supervision (code, tool calls) |
| R5 | Error-, critique-, or revision-aware supervision |

Full definitions with typical signals and examples are in `TAXONOMY.md`.

## Inclusion-status rule (important, easy to get wrong)

`Inclusion Status` in `data/inventory.csv` is *derived* from `Supervision
Level`, not an independent judgment call:

- **Pure R0** (nothing in the resource carries an explicit reasoning
  representation) → out of scope. Remove the row entirely from
  `data/inventory.csv` and add it to the "Excluded: no explicit reasoning"
  list in `TAXONOMY.md` with a one-line reason. Do not keep it in the CSV
  under a "historical context only" label.
- **Mixed R0/R1+** (a real, verified subset of the resource carries
  explicit reasoning, even if most items don't) → stays in, as Borderline
  or better.
- **R1 and above, verified** → Include / Likely include, depending on how
  well-verified the representation and its construction/validation are.
- **Training-resource-only** entries (e.g. MegaScience, TextbookReasoning)
  are a *different* exclusion axis — they do carry real R2/R3 reasoning
  representations and stay in the inventory; they're flagged only because
  they're training data rather than an evaluation benchmark. Don't remove
  these the way pure-R0 entries are removed.

When verifying a Borderline/Low-confidence row and it turns out to be pure
R0, remove it and log it under "Excluded" — this is a mechanical
consequence of the rule above, not a fresh decision to deliberate each time.

## Adding or editing an inventory entry

Follow `CONTRIBUTING.md`:

1. One row per dataset/benchmark in `data/inventory.csv` (if a paper
   introduces several, add each separately), following the existing
   column set — see `TAXONOMY.md` / `data/coding_dimensions.csv` for what
   each column means and suggested values.
2. Fill in fields from a skim of the paper; use `N/A` for fields that
   genuinely don't apply, leave truly unknown fields blank — don't guess.
3. If unsure whether an entry clears the scope bar (explicit reasoning,
   not just final-answer QA), add it anyway with `Evidence Confidence: Low`
   and note the doubt in `Key Limitation` rather than omitting it —
   resolve it on review via the inclusion-status rule above.
4. No need to pre-sort entries into a top-level category — the
   public-facing grouping is applied separately (see open decision below).

## Open decision

The README's public-facing list is not yet sorted/grouped — candidates are
Scientific Domain, Primary Task, or Supervision Level (R0–R5); noted at the
bottom of `TAXONOMY.md`. Don't assume one of these has been chosen unless
`README.md` has been updated to reflect it.
