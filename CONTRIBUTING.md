# Contributing

PRs adding relevant datasets/benchmarks are welcome.

## Adding an entry

1. Add your entry to [`PAPERS.md`](PAPERS.md) under `## Entries`, following
   the format documented at the top of that file.
2. Fill in as many of the `domain` / `construction` / `representation` /
   `validation` / `errors` tags as you can from a skim of the paper; leave
   the rest as `?`.
3. One entry per dataset/benchmark. If a paper introduces more than one,
   add each separately.
4. Open a PR. No need to sort into a category — sorting into the final
   taxonomy happens separately once we've settled it (see
   [`TAXONOMY.md`](TAXONOMY.md)).

## Scope

In scope: datasets and benchmarks that involve **explicit** scientific
reasoning — i.e., the reasoning process itself (not just the final answer)
is represented, supervised, or evaluated in some way. General QA/knowledge
benchmarks without an explicit reasoning component are out of scope.
