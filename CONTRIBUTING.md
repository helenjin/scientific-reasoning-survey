# Contributing

PRs adding relevant datasets/benchmarks are welcome.

## Adding an entry

1. Add a row to [`data/inventory.csv`](data/inventory.csv), following its
   existing columns (task, domain, modality, reasoning representation,
   supervision level, construction, validation, error-annotation fields,
   etc.) — see [`TAXONOMY.md`](TAXONOMY.md) for what each column means and
   the recommended values.
2. Fill in as many fields as you can from a skim of the paper; use `N/A`
   for fields that don't apply and leave genuinely unknown fields blank
   rather than guessing.
3. One row per dataset/benchmark. If a paper introduces more than one,
   add each separately.
4. Open a PR. No need to pre-sort into a category — the public-facing
   grouping is applied separately once the top-level organization is
   settled (see the open decision noted in [`TAXONOMY.md`](TAXONOMY.md)).

## Scope

In scope: datasets and benchmarks that involve **explicit** scientific
reasoning — i.e., the reasoning process itself (not just the final answer)
is represented, supervised, or evaluated in some way. General QA/knowledge
benchmarks without an explicit reasoning component (pure R0 — see
[`TAXONOMY.md`](TAXONOMY.md)) are out of scope: don't add them as a coded
row, even if well-known. If you're unsure whether something clears the
bar, add it anyway with `Evidence Confidence: Low` and note the doubt in
`Key Limitation` — verification during review will resolve it.
