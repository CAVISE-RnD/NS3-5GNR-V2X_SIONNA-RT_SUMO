# Repository guide

## Manuscript entry points

| Path | Purpose |
|---|---|
| [`README.md`](README.md) | Framework overview, architecture, quick start, and citation guidance |
| [`reproducibility_package/`](reproducibility_package/README.md) | Retained manuscript data, source snapshots, analysis, and checksum validation |
| [`CITATION.cff`](CITATION.cff) | Machine-readable citation metadata for this research overlay |
| [`DEVELOPMENT.md`](DEVELOPMENT.md) | Analysis environment, simulator bootstrap, and test guidance |
| [`CONTRIBUTING.md`](CONTRIBUTING.md) | Issue reporting, contributions, and preservation of experimental evidence |

## Source and experiment directories

| Path | Purpose |
|---|---|
| [`src/`](src/) | ns-3/ms-van3t/VaN3Twin overlay, communication applications, and integration modules |
| [`experiments/`](experiments/README.md) | Scenario launchers, configurations, scenes, and protocols |
| [`runs/`](runs/README.md) | Additional retained development and experiment records |
| [`tools/`](tools/README.md) | Analysis, plotting, aggregation, scenario management, and historical authoring utilities |
| [`tests/`](tests/) | Research-analysis tests and simulator fixtures |
| [`scripts/`](scripts/) | Build, environment, and publication-packaging utilities |
| [`docker/`](docker/) | Container definitions |
| [`docs/`](docs/) | Inherited framework documentation and supplementary technical notes |
| [`emulation-support/`](emulation-support/) | Upstream emulation and CARLA/OpenCDA integration support |
| [`img/`](img/) | Framework graphics and retained figures |
| [`.github/`](.github/) | Manuscript-analysis CI and issue/pull-request templates |

## Other root files

`LICENSE`, `license_gplv2.txt`, and `AUTHORS` retain upstream licensing and attribution. `CHANGES.md` and `RELEASE_NOTES.md` contain inherited framework history. `Makefile`, `sandbox_builder.sh`, `adapt_files.py`, and the integration shell scripts support simulator setup. The legacy bootstrap modifies its working directory; use the disposable workflow in [DEVELOPMENT.md](DEVELOPMENT.md).

## Where to add new work

Place new scenarios under `experiments/<name>/`, analysis under `tools/analysis/`, and plots under `tools/plots/`. Keep new campaign records in a separate, identified output location with commands, seeds, source versions, and environment provenance. Do not overwrite the retained manuscript sample or mix prospective cohorts into its analysis.

Virtual environments, build trees, generated analysis output, editor metadata, and assistant-specific files are local working materials and are excluded from new commits. Existing tracked evidence and required upstream assets remain part of the repository.
