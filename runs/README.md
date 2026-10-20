# Retained run records

This directory preserves records from development and experiment runs, usually organized by date and scenario. Contents may include logs, CSV tables, figures, configuration records, and run reports. Availability and schemas vary across campaigns.

For the exact retained sample used in the manuscript analysis, use [`reproducibility_package/`](../reproducibility_package/README.md). It defines the 140 EVA runs and 27 complete-case intersection runs, validates the packaged input checksums, and documents missing records and selection criteria. Do not infer that every run in this directory belongs to that sample.

## Working with records

Read each run's configuration and report before comparing results. Keep the original records unchanged, place derived outputs in a separate directory, and retain the source commit, commands, seeds, and environment information for any new campaign.

General analysis and plotting utilities are under [`tools/`](../tools/README.md); scenario-specific processing may also be provided under `experiments/<name>/tools/`. Historical directory names are preserved so that existing scripts and provenance references continue to resolve.
