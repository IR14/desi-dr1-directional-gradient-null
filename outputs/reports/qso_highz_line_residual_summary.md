# QSO high-z emission-line residual gradient summary

Status: active null on the tested QSO line observables.

This follow-up tests whether high-redshift QSO emission-line residuals show a coherent sky dipole after redshift, luminosity proxies, line-fit diagnostics, survey geometry, and external imaging templates are controlled.

## Inputs

- LSS sample: `data/interim/qso_ngc_sgc_highz_1p5_3p5_lss.parquet`
- VAC: `data/raw/vac/fastspecfit/iron/v2.1/catalogs/fastspec-iron-main-dark.fits`
- Random catalogs: `QSO_NGC_0_clustering.ran.fits`, `QSO_SGC_0_clustering.ran.fits`
- Redshift range: `1.5 <= z < 3.5`
- HEALPix: `nside=16`
- Block null: `500` spatial block permutations, `block_nside=2`
- External templates: EBV, stellar density, g/r/z depth, g/r/z PSF size, g/r/z sky brightness

## Quality-cut adjustment

The initial line-observable run failed because the generic FastSpecFit line-quality threshold `DELTA_LINECHI2 > 25` is not appropriate as a hard cut for the high-z QSO VAC line columns. In the audited joined sample of 799,010 objects, that threshold left only 55 usable CIV rows and 68 usable CIII rows after finite-observable, positive-IVAR, and ZWARN cuts. The pipeline now treats `RCHI2_LINE` and `DELTA_LINECHI2` as residual-model controls for line observables, while retaining hard cuts on `ZWARN == 0`, finite observable values, positive observable IVAR, and winsorization.

## Results

| observable | joined rows | amplitude | axis RA deg | axis DEC deg | fitted pixels | block-null p-value |
|:--|--:|--:|--:|--:|--:|--:|
| `CIV_1549_EW` | 761,395 | 0.303061 | 85.281 | 7.464 | 1003 | 0.958084 |
| `CIII_1908_EW` | 758,337 | 0.148250 | 132.129 | -42.987 | 1004 | 0.904192 |

The CIV and CIII fitted axes are separated by 65.953 degrees. The directions are therefore not mutually stable, and both block-null p-values are high.

## Interpretation

This run does not support a coherent high-redshift QSO emission-line residual dipole. The measured amplitudes are not anomalous under spatial block shuffling, and the two independent line observables do not point to a common axis.

The scientifically conservative status remains: no robust directional gradient detected in the tested DESI DR1 QSO high-z observables.

## Artifacts

- `outputs/reports/qso_highz_line_civ_1549_ew_gradient.md`
- `outputs/reports/qso_highz_line_ciii_1908_ew_gradient.md`
- `outputs/tables/qso_highz_line_civ_1549_ew_gradient.csv`
- `outputs/tables/qso_highz_line_ciii_1908_ew_gradient.csv`
- `outputs/figures/qso_highz_line_civ_1549_ew_gradient_residual_vs_z.png`
- `outputs/figures/qso_highz_line_civ_1549_ew_gradient_residual_hist.png`
- `outputs/figures/qso_highz_line_ciii_1908_ew_gradient_residual_vs_z.png`
- `outputs/figures/qso_highz_line_ciii_1908_ew_gradient_residual_hist.png`

## Verification

- `uv run pytest tests/test_fastspecfit.py`: 7 passed
- `uv run pytest`: 35 passed
