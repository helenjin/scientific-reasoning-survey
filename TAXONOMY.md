# Taxonomy notes (working log)

Decision on how to organize `PAPERS.md` / the README's dataset-and-benchmark
list is **deferred** until the list is compiled and we can see what
categories the actual entries fall into. This file logs the candidate
organizing axes discussed so far, so the decision isn't lost.

## Candidate top-level axes

1. **Scientific domain** — Math, Physics, Chemistry, Biology,
   Multi-domain/General Science. Simplest for readers browsing by field;
   mirrors how most existing benchmark papers self-identify.
2. **Construction method** — human-expert curated, synthetic/procedurally
   generated, LLM-generated, derived from formal proofs/simulations.
   Matches one of the survey's core analytical dimensions.
3. **Reasoning representation** — free-text CoT, structured/symbolic steps,
   program-based, proof-based. Matches another core analytical dimension.

## Other dimensions the survey analyzes (per entry, regardless of top-level axis)

These should end up as *columns/tags* on each entry no matter which axis
wins, since they're the actual analytical content of the survey:

- Motivation (why the dataset/benchmark was built)
- Task type (QA, generation, verification, error-detection, ...)
- Reasoning representation (see above)
- Construction method (see above)
- Validation strategy (how correctness/quality was checked)
- Error annotation (whether/how reasoning errors are labeled)

## Status

Compiling the flat list first (see `PAPERS.md`). Revisit this file once we
have enough entries to see which axis produces the cleanest split (target:
no bucket with only 1-2 entries, no bucket with a large majority of all
entries).
