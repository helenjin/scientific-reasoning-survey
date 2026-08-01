# Datasets & Benchmarks — working list

This is a **flat, unsorted** collection log of datasets/benchmarks for
explicit scientific reasoning. Entries live here until we've compiled
enough to settle the top-level taxonomy (see [`TAXONOMY.md`](TAXONOMY.md));
they'll then be sorted into `README.md` under whichever axis we pick.

## Entry format

```markdown
1. **Dataset/Paper title** `Venue Year` [[paper]](https://...) [[data]](https://...)

   *Author One, Author Two, Author Three*

   `domain:` `construction:` `representation:` `validation:` `errors:`
```

- `domain` — scientific domain(s) covered (math, physics, chemistry, biology, multi-domain, ...)
- `construction` — how it was built (human-expert, synthetic/procedural, LLM-generated, derived-from-proofs/simulations, ...)
- `representation` — how reasoning is represented/supervised (free-text CoT, structured/symbolic, program-based, proof-based, ...)
- `validation` — how correctness/quality was checked (expert review, automatic verifier, self-consistency, none reported, ...)
- `errors` — whether/how reasoning errors are annotated (none, taxonomy of error types, free-text critique, ...)

Leave any tag as `?` if not yet determined from a skim of the paper — fill
it in on a closer pass rather than blocking on it.

## Entries

<!-- Add entries below, one per dataset/benchmark. No sub-sections yet — see TAXONOMY.md for why. -->
