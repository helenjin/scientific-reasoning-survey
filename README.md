<h1 align="center">Awesome Scientific Reasoning Datasets & Benchmarks</h1>

<p align="center">
  <a href="https://github.com/sindresorhus/awesome"><img src="https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg"></a>&nbsp;
  <a href="https://github.com/helenjin/scientific-reasoning-survey/stargazers"><img src="https://img.shields.io/github/stars/helenjin/scientific-reasoning-survey?style=social"></a>&nbsp;
  <a href="https://opensource.org/licenses/MIT"><img src="https://img.shields.io/badge/License-MIT-yellow.svg"></a>&nbsp;
  <a href="https://github.com/helenjin/scientific-reasoning-survey/pulls"><img src="https://img.shields.io/badge/PRs-Welcome-red"></a>
</p>

<!-- TODO: add an arXiv badge here once the survey paper is posted, e.g.
  <a href="https://arxiv.org/abs/XXXX.XXXXX"><img src="https://img.shields.io/badge/arXiv-XXXX.XXXXX-b31b1b.svg"></a>
-->

This repo accompanies a survey providing the first systematic
characterization of datasets and benchmarks for **explicit scientific
reasoning**. We review how scientific reasoning is represented, supervised,
and evaluated across NLP and ML resources — analyzing their underlying
motivations, tasks, reasoning representations, construction methods,
validation strategies, and error annotations — to identify gaps and future
research directions.

## Citation

<!-- TODO: fill in once the paper has an arXiv ID / venue -->

```bibtex
@article{jinscientificreasoningsurvey,
  title={A Survey of Datasets and Benchmarks for Explicit Scientific Reasoning},
  author={Jin, Helen},
  journal={TBD},
  year={2026}
}
```

## Contents

- [Datasets & Benchmarks](#datasets--benchmarks)
- [Taxonomy](#taxonomy)
- [Contributing](#contributing)
- [License](#license)

## Datasets & Benchmarks

The full, flat list of coded datasets/benchmarks lives in
[`data/inventory.csv`](data/inventory.csv) (53 entries as of writing) — one
row per resource, coded across task, domain, modality, reasoning
representation, construction, validation, and error-annotation fields (see
[Taxonomy](#taxonomy)).

A public-facing sorted/rendered version of this list (e.g. grouped by domain
or by reasoning-representation level) will replace this section once the
top-level organization is settled — see the open decision noted at the
bottom of [`TAXONOMY.md`](TAXONOMY.md).

## Taxonomy

The coding scheme used to annotate `data/inventory.csv` — reasoning
representation levels (R0–R5), per-entry coding dimensions, task
definitions, and error-annotation fields — is documented in
[`TAXONOMY.md`](TAXONOMY.md), backed by machine-readable CSVs under
[`data/`](data/).

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md) — PRs adding datasets/benchmarks
are welcome.

## License

[MIT](LICENSE)
