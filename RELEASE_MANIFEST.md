# Release Manifest

Package: `desi-dr1-directional-gradient-null`  
Prepared: 2026-05-28

## Included

- `paper/main.tex`: English manuscript source.
- `paper/main_ru.tex`: Russian working translation.
- `src/cosmo_gradient/`: analysis package used for the DESI DR1 checks.
- `tests/`: pytest suite.
- `configs/default.yaml`: default runtime configuration.
- `outputs/reports/`: selected final reports cited by the manuscript.
- `outputs/tables/`: selected small CSV result tables.
- `outputs/figures/`: selected diagnostic figures.
- `README.md`, `CITATION.cff`, `.zenodo.json`, `LICENSE`, `.gitignore`.

## Excluded

- raw DESI FITS/Parquet files;
- external SSD data;
- local virtual environments;
- logs, PID files, and caches;
- exploratory number-theory/model-development reports;
- conversation or assistant-specific artifacts.

## Verification

Executed from this release directory:

```bash
uv run --extra test --extra desi --extra healpix --extra science pytest
```

Result:

```text
35 passed
```

LaTeX structural check:

```text
paper/main.tex: balanced document/table/math environments
paper/main_ru.tex: balanced document/table/math environments
```

No files larger than 10 MB are included.

