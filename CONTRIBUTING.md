# Contributing

Contributions should make the framework easier to use, test, and reproduce. Keep changes focused and explain their effect on simulation behavior or reported results.

## Reporting a problem

Open an issue with the full commit SHA, operating system, relevant dependency versions, exact command, and expected and observed behavior. For a simulation issue, include the scenario, random seed and run identifier, enabled channel model, and a small relevant log excerpt. For a manuscript-analysis issue, include the output of `reproducibility_package/analyze.py` and any failing checksum or assertion.

## Development workflow

1. Create a branch from the current `main` revision.
2. Follow [DEVELOPMENT.md](DEVELOPMENT.md) for the environment needed by the change.
3. Preserve upstream directory structure, copyright notices, and license files.
4. Run the relevant existing checks and describe their outcome in the pull request.
5. Update documentation when commands, outputs, or supported behavior change.

## Experimental evidence

Keep the manuscript sample, historical source snapshots, and prospective experiments distinct. Do not replace retained observations with newly simulated data under the same identifiers. Changes to metric definitions, selection criteria, source snapshots, or input archives need an explicit rationale and a corresponding update to the analysis documentation.

The four archives in `reproducibility_package/` are checksum-verified by the analysis script. Treat a checksum failure as a change to the evidence, not as an instruction to silently regenerate the expected digest. Keep run-level provenance, failed-run reasons, and source/environment versions with any new campaign.

## Validation

For manuscript data or analysis changes, run from the repository root:

```bash
python -m pip install -r reproducibility_package/requirements.txt
python reproducibility_package/analyze.py --output results.json
```

Use a virtual environment and run without Python's `-O` flag. GitHub Actions runs this analysis on Python 3.11 and 3.12. Simulator changes additionally require a build and tests appropriate to the affected module; a passing data-analysis check alone does not validate simulator behavior.

Do not commit local virtual environments, build outputs, credentials, editor metadata, assistant instructions, or generated analysis output. Preserve the manuscript records already tracked in Git. Use small, relevant fixtures for new tests.

## Attribution

Retain the existing GPL notices and third-party license terms. Identify the upstream origin of imported code. Use [CITATION.cff](CITATION.cff) and the README citation guidance when referencing the research overlay or its reproducibility package.
