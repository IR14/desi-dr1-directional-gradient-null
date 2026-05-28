# DESI DR1 Directional-Gradient Null Result

This repository package contains the manuscript source, analysis code, and
small derived artifacts for:

**A DESI DR1 Search for Directional Gradients in Galaxy Population and
High-Redshift Quasar Observables**

Author: I. Mikhailov  
Date: 2026-05-28

## Scope

This is a reproducible observational null-result package. It tests whether
public DESI DR1 LSS and FastSpecFit observables show a repeatable large-scale
directional dipole after accounting for survey geometry, random catalogs,
redshift trends, nuisance variables, external imaging templates, and spatial
block-null tests.

The result is an active null:

- controlled observational family minimum block-null p-value: `p = 0.4091816367`;
- preregistered QSO line-ratio primary family minimum p-value: `p = 0.8802395209`;
- no repeated directional axis across the tested DR1 tracer/property families.

The package intentionally excludes raw DESI FITS/Parquet data and large mock
catalogs.

## Repository Contents

```text
paper/
  main.tex        # English manuscript source
  main_ru.tex     # Russian working translation

src/
  cosmo_gradient/ # Python analysis package

tests/            # pytest coverage for coordinates, maps, dipoles, mocks, FastSpecFit
configs/          # default configuration

outputs/
  reports/        # selected final reports used by the manuscript
  tables/         # selected small CSV result tables
  figures/        # selected diagnostic figures
```

## Data Availability

Raw data are not redistributed here. Reproduction of the full production runs
requires downloading the relevant public DESI DR1 products:

- DESI DR1 documentation: <https://data.desi.lbl.gov/doc/releases/dr1/>
- DESI DR1 LSS catalogs: <https://data.desi.lbl.gov/public/dr1/survey/catalogs/dr1/LSS/iron/LSScats/v1.5/>
- FastSpecFit documentation: <https://fastspecfit.readthedocs.io/en/2.1.2/>
- DESI DR1 AGN/QSO VAC documentation: <https://data.desi.lbl.gov/doc/releases/dr1/vac/agnqso/>

Expected local raw-data paths follow the original project convention:

```text
data/raw/
  LRG_NGC_clustering.dat.fits
  LRG_NGC_0_clustering.ran.fits
  QSO_NGC_clustering.dat.fits
  QSO_SGC_clustering.dat.fits
  QSO_NGC_0_clustering.ran.fits
  QSO_SGC_0_clustering.ran.fits
  vac/fastspecfit/iron/v2.1/catalogs/fastspec-iron-main-dark.fits
```

Large files may also be stored outside the repository and referenced through
`configs/default.yaml`.

## Installation

Python 3.13 is expected. The original analysis used `uv`.

```bash
cd desi-dr1-directional-gradient-null
uv sync --extra test --extra plot --extra desi --extra healpix --extra science
```

If `healpy` is unavailable on your platform, omit `--extra healpix` for basic
code inspection and tests. Scientific sky-map production runs should use the
HEALPix backend.

Run tests:

```bash
uv run pytest
```

## Compile the Manuscript

Using a local TeX installation:

```bash
cd paper
pdflatex -interaction=nonstopmode main.tex
pdflatex -interaction=nonstopmode main.tex
```

The same `paper/main.tex` can be uploaded directly to Overleaf.

## Reproduction Commands

The selected result files under `outputs/` are small derived artifacts from the
production run. To rerun the principal LRG FastSpecFit residual test after
placing DESI DR1 files under `data/raw/`:

```bash
uv run cosmo-gradient fastspecfit-gradient \
  --lss data/raw/LRG_NGC_clustering.dat.fits \
  --vac data/raw/vac/fastspecfit/iron/v2.1/catalogs/fastspec-iron-main-dark.fits \
  --random data/raw/LRG_NGC_0_clustering.ran.fits \
  --observable DN4000_MODEL \
  --z-min 0.4 \
  --z-max 0.6 \
  --nside 16 \
  --block-null-mocks 500 \
  --block-nside 2 \
  --min-objects-per-pixel 15 \
  --seed 20260527 \
  --output-prefix outputs/tables/desi_fastspecfit_gradient_validation
```

Other QSO density, line-equivalent-width, and line-ratio results require the
same DESI DR1 QSO LSS catalogs, FastSpecFit VAC, and external imaging-template
maps used in the original local run. The included reports and CSV files provide
the audited outputs for the manuscript.

## Citation

Please cite the archived software release and the accompanying preprint when
using this package. Citation metadata are provided in `CITATION.cff`. If a
Zenodo DOI is available for the release, prefer the DOI over a plain repository
URL.

## Scientific Interpretation

This package does not claim proof of exact cosmic isotropy. It reports that the
specific DESI DR1 directional-gradient signatures tested here are not detected
under the implemented corrections. Further searches on the same DR1 data should
be avoided unless new data, official property mocks, a methodological bug fix,
or a preregistered new observable family changes the analysis scope.
