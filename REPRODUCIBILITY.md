# Reproducibility Guide

This repository is the full research workspace. Public paper reproduction is organized through two compact release repositories so that readers do not need the mixed experiment history or raw cloud traces.

## Supported Paper Releases

| Paper | Repository | CPU check |
|---|---|---|
| Same Targets, Different Computation | `yifan1207/first-divergence-crosspatching` | `python scripts/reproduce/check_same_base_dependencies_paper.py` |
| The Convergence Gap | `yifan1207/convergence-gap-instruction-tuning` | `python scripts/reproduce/check_convergence_gap_claims.py` |

Each release contains the paper PDF, compact CSV/JSON evidence, a claim-to-artifact map, figure scripts, and a SHA-256 manifest.

## Reproduction Levels

### 1. Compact claim check

Use the paper release repository. The checker recomputes reported values from committed summaries on CPU, normally in seconds.

### 2. Figure regeneration

Install the release's small `requirements.txt` and run its paper-facing plotting script. This reproduces the displayed figures from committed summaries without loading a language model.

### 3. Raw-shard audit

Selected experiments retain enough provenance to validate the record schema, intervention cells, model revisions, and aggregation code on a small raw shard. These audits require external raw data and, when regenerated, a large-memory GPU.

### 4. Full rerun

Full experiments require gated model access, model-family-specific adapters, and A100/H100-class GPUs. Launchers live under `scripts/run/`; experiment implementations live under `src/poc/exp##_descriptive_name/`.

## Workspace Setup

```bash
uv sync
uv run python scripts/infra/repo_doctor.py
```

The repository uses descriptive experiment paths:

```text
src/poc/exp##_descriptive_name/
results/exp##_descriptive_name/
scripts/{run,analysis,plot,reproduce,infra}/
```

## Data Policy

Git contains code, fixed evaluation manifests, compact paper-facing summaries, and selected plots. It intentionally excludes model weights, adapters, activation caches, step-level training logs, and multi-gigabyte raw intervention traces. Large raw artifacts are stored separately and are not required for the CPU claim checks.

## Provenance

The paper releases record:

- checkpoint identifiers and pinned revisions;
- fixed prompt manifests and support definitions;
- paper-facing CSV/JSON summaries;
- claim-to-artifact mappings;
- deterministic claim checkers;
- file hashes.

The full workspace contains additional exploratory and superseded experiments. Those should not be treated as part of a paper's evidence chain unless they appear in the corresponding release artifact map.
