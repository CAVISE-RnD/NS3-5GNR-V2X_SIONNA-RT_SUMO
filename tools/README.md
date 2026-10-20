# Analysis and development tools

These utilities support scenario development, record inspection, plotting, and publication preparation. The self-contained entry point for the retained manuscript results is [`reproducibility_package/analyze.py`](../reproducibility_package/analyze.py).

| Directory | Purpose |
|---|---|
| [`analysis/`](analysis/) | Run inspection, metric extraction, campaign aggregation, and data export |
| [`plots/`](plots/) | Figures, event timelines, animations, and scene visualization |
| [`results_pipeline/`](results_pipeline/) | Structured result ingestion and aggregation |
| [`scenario_manager/`](scenario_manager/) | Scenario launch and sweep management |
| [`vkr/`](vkr/) | Historical document and figure authoring utilities retained for provenance |

Scenario-specific utilities may also live under `experiments/<name>/tools/`. Each utility has its own input and dependency requirements; the minimal manuscript-analysis environment is not intended to cover every plotting or simulation tool.

Use separate output directories for new analyses, preserve input records, and record the full repository commit SHA. See [DEVELOPMENT.md](../DEVELOPMENT.md) for environments and [CONTRIBUTING.md](../CONTRIBUTING.md) for validation and evidence-handling guidance.
