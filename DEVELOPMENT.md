# Development and simulation setup

The manuscript analysis and the simulator use different environments. Start with the [reproducibility package](reproducibility_package/README.md) if your goal is to verify the retained manuscript results; it needs only Python and NumPy.

Simulator development requires Linux, a C++ toolchain, SUMO, and the appropriate ns-3/5G-LENA dependencies. Sionna-enabled scenarios also require a compatible ray-tracing environment. Use a case-sensitive filesystem: some inherited ASN.1 filenames differ only by case. On Windows, use the Linux filesystem inside WSL or a Linux Docker volume for the build.

## Manuscript analysis

From the repository root, using Python 3.11 or later in a virtual environment:

```bash
python -m pip install -r reproducibility_package/requirements.txt
python reproducibility_package/analyze.py --output results.json
```

The package verifies input checksums and validates 140 EVA runs, 27 intersection runs, 281 CAM-control links, and 81 complete raw EVA MSG sets. Do not enable Python optimization with `-O`.

## Build a simulator in a disposable directory

Clone the repository on a Linux filesystem:

```bash
git clone https://github.com/CAVISE-RnD/Sionna_SUMO_simu.git
cd Sionna_SUMO_simu
```

The inherited `sandbox_builder.sh` rewrites its working directory, including Git metadata. Use the provided wrapper to run it in a separate disposable clone. Choose a destination that does not already exist:

```bash
bash scripts/bootstrap-disposable.sh --destination "$HOME/v2x-simulator-build" --dry-run
bash scripts/bootstrap-disposable.sh --destination "$HOME/v2x-simulator-build" --install-dependencies
```

The dependency installation may request system privileges. If dependencies are already installed, omit `--install-dependencies`. The wrapper copies committed source through a local clone; use its documented `--copy-source` option only when deliberately including uncommitted development changes.

Configure and build the generated ns-3 tree:

```bash
cd "$HOME/v2x-simulator-build/repo/ns-3-dev"
./ns3 configure --build-profile=optimized --enable-examples --enable-tests --disable-python --disable-werror
./ns3 build -j 2 v2v-simple-cam-exchange-80211p
./ns3 run --no-build "v2v-simple-cam-exchange-80211p"
```

This is an upstream installation smoke test, not a reproduction of the manuscript campaigns. Build the targets required by your scenario or run `./ns3 build -j 2` for the full enabled build. Reduce parallelism if memory is limited.

## Pinned research environment

[`docker/Dockerfile.research`](docker/Dockerfile.research) records an Ubuntu 22.04 image digest and pinned Python packages, including Sionna 1.0.0. [`scripts/research/bootstrap.py`](scripts/research/bootstrap.py) assembles recorded ns-3, NR, and base-overlay revisions into a separate Linux build directory and writes an environment manifest. Its `--patch-source` option copies an explicit list of research files; it is not a generic synchronization of every file in the current checkout.

Build the container from the repository root:

```bash
docker build -f docker/Dockerfile.research -t v2x-research .
```

Inside the research container, mount this repository read-only at `/source` and provide a writable Linux volume at `/research`. The source-assembly command is:

```bash
python3 /source/scripts/research/bootstrap.py --root /research --patch-source /source
```

Configure and build `/research/ns-3-dev` for the selected experiment. A Sionna-enabled run additionally needs compatible GPU/driver/OptiX access and the selected scene configuration. Record the actual image digest, dependency versions, hardware, scene hashes, and run arguments. This route supports the separate prospective work documented in [`experiments/future_transport_2026/PROTOCOL.md`](experiments/future_transport_2026/PROTOCOL.md); it is not an exact historical campaign replay.

## Tests

The [GitHub Actions workflow](.github/workflows/reproducibility.yml) checks the manuscript analysis on Python 3.11 and 3.12. The Python research tests are under [`tests/research/`](tests/research/); install the dependencies needed by the selected tests in your development environment.

Inside a configured ns-3 tree, use the upstream test runner:

```bash
./test.py --list
./test.py --no-build --suite=<suite-name>
```

`./ns3 test` is not the test command for this tree. Simulator changes require checks for the affected module in addition to the independent manuscript-data analysis.

## Common setup issues

- **Missing `ns3`:** the executable belongs to the generated simulator tree, not the overlay root.
- **Compiler killed:** reduce build jobs and inspect available memory.
- **Files missing or overwritten on Windows:** use a case-sensitive Linux filesystem for source assembly and compilation.
- **Channel-service failure:** check the configured Sionna endpoint, scene, runtime dependencies, and simulator log; retain fallback and failure records with the run.
- **Version mismatch:** record the actual SUMO/TraCI and ns-3/NR revisions. The inherited documentation's compatibility notes do not certify every newer release.

Preserve the original input archives and historical source metadata when investigating a reproducibility issue. See [CONTRIBUTING.md](CONTRIBUTING.md) for reporting and validation guidance.
