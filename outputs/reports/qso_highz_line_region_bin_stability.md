# QSO high-z line residual region/bin stability

Status: active null remains stable after splitting by survey region and redshift bin.

This run stress-tests the QSO emission-line residual result by splitting the `1.5 <= z < 3.5` sample into NGC/SGC and two redshift bins. The estimator is unchanged from the combined line-residual run: line equivalent-width residuals are fit after controls for redshift, luminosity proxies, line-fit diagnostics, survey geometry, and external imaging templates, then projected to HEALPix `nside=16` with IVAR weighting and tested against 500 spatial block permutations.

## Cached inputs

- `data/interim/qso_ngc_highz_1p5_3p5_lss.parquet`: 518,744 rows
- `data/interim/qso_sgc_highz_1p5_3p5_lss.parquet`: 280,274 rows
- `data/interim/qso_highz_1p5_3p5_fastspecfit_line_vac.parquet`: 799,010 rows

The VAC cache avoids repeated full reads of the 40 GB FastSpecFit FITS file and contains only the high-z QSO target IDs and line-analysis columns.

## Results

| region | zbin | observable | n_joined | amplitude | axis RA deg | axis DEC deg | block-null p-value |
|:--|:--|:--|--:|--:|--:|--:|--:|
| NGC | z1p5_2p1 | `CIII_1908_EW` | 264,221 | 0.129588 | 62.562 | -53.136 | 0.972056 |
| NGC | z1p5_2p1 | `CIV_1549_EW` | 266,722 | 0.831954 | 23.369 | -26.754 | 0.816367 |
| NGC | z2p1_3p5 | `CIII_1908_EW` | 228,933 | 0.207706 | 125.004 | -79.184 | 0.942116 |
| NGC | z2p1_3p5 | `CIV_1549_EW` | 228,136 | 0.452652 | 32.986 | -45.106 | 0.954092 |
| SGC | z1p5_2p1 | `CIII_1908_EW` | 141,485 | 0.087681 | 13.246 | -65.582 | 0.996008 |
| SGC | z1p5_2p1 | `CIV_1549_EW` | 142,895 | 0.625780 | 341.211 | -0.809 | 0.988024 |
| SGC | z2p1_3p5 | `CIII_1908_EW` | 123,698 | 0.267788 | 175.376 | 52.217 | 0.966068 |
| SGC | z2p1_3p5 | `CIV_1549_EW` | 123,642 | 0.541443 | 181.244 | 44.024 | 0.990020 |

## Axis consistency

| region | zbin | CIV/CIII axis separation |
|:--|:--|--:|
| NGC | z1p5_2p1 | 39.165 deg |
| NGC | z2p1_3p5 | 46.277 deg |
| SGC | z1p5_2p1 | 68.699 deg |
| SGC | z2p1_3p5 | 9.075 deg |

The only close line-pair axis is `SGC z2p1_3p5`, but both corresponding block-null p-values are extremely high (`0.966` and `0.990`). This is not evidence for an anomalous axis.

## Interpretation

The region/bin split finds no low-p outlier. The smallest block-null p-value in the full 8-cell grid is `0.816`, so every measured amplitude is common under spatial block shuffling.

This strengthens the previous QSO high-z conclusion: no robust directional gradient is detected in the tested DESI DR1 high-redshift QSO emission-line residuals.

## Artifacts

The per-cell CSV, markdown, and figure artifacts are written under:

- `outputs/tables/qso_highz_line_<region>_<zbin>_<observable>_gradient.csv`
- `outputs/reports/qso_highz_line_<region>_<zbin>_<observable>_gradient.md`
- `outputs/figures/qso_highz_line_<region>_<zbin>_<observable>_gradient_residual_vs_z.png`
- `outputs/figures/qso_highz_line_<region>_<zbin>_<observable>_gradient_residual_hist.png`
