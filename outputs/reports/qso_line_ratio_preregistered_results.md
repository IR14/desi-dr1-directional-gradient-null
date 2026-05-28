# QSO line-ratio preregistered results

Created: 2026-05-28

Status: active null.

This report executes the frozen protocol from:

- `outputs/reports/qso_line_ratio_preregistration.md`

No additional line ratios, cuts, bins, or interpretation rules were added during the first execution.

## Derived VAC Cache

Created:

- `data/interim/qso_highz_1p5_3p5_fastspecfit_line_ratio_vac.parquet`

Input high-z QSO VAC rows: 799,010.

Derived primary observables:

| observable | eligible finite-positive rows | median value |
|:--|--:|--:|
| `LOG_CIV_CIII_EW` | 758,235 | 1.09124 |
| `LOG_CIV_MGII2796_EW` | 607,835 | 1.33879 |
| `LOG_CIII_MGII2796_EW` | 603,983 | 0.163066 |

The ratio inverse-variance weights use the preregistered propagation rule for `ln(x/y)`.

## Primary Family

Primary family size: `m = 6`.

| zbin | observable | rows | amplitude | axis RA deg | axis DEC deg | block-null p-value |
|:--|:--|--:|--:|--:|--:|--:|
| z1p5_2p1 | `LOG_CIV_CIII_EW` | 396,908 | 0.005927 | 90.086 | 13.236 | 0.970060 |
| z1p5_2p1 | `LOG_CIV_MGII2796_EW` | 407,103 | 0.002747 | 149.263 | -31.179 | 0.994012 |
| z1p5_2p1 | `LOG_CIII_MGII2796_EW` | 403,644 | 0.005951 | 251.516 | 25.093 | 0.980040 |
| z2p1_3p5 | `LOG_CIV_CIII_EW` | 345,404 | 0.004468 | 171.736 | 10.948 | 0.980040 |
| z2p1_3p5 | `LOG_CIV_MGII2796_EW` | 186,086 | 0.017718 | 174.848 | -54.049 | 0.880240 |
| z2p1_3p5 | `LOG_CIII_MGII2796_EW` | 186,114 | 0.012246 | 109.881 | 27.207 | 0.980040 |

Minimum primary p-value:

- `p_min = 0.8802395209580839`
- test: `z2p1_3p5 / LOG_CIV_MGII2796_EW`

Look-elsewhere sanity checks:

| correction | value |
|:--|--:|
| Bonferroni `min(1, 6 * p_min)` | 1.000000 |
| Sidak `1 - (1 - p_min)^6` | 0.999997 |

No primary ratio test approaches the preregistered weak diagnostic threshold (`p < 0.05`).

## Stability Suite

Stability suite size: `m = 12`.

Lowest stability p-values:

| region | zbin | observable | rows | amplitude | axis RA deg | axis DEC deg | block-null p-value |
|:--|:--|:--|--:|--:|--:|--:|--:|
| SGC | z2p1_3p5 | `LOG_CIV_CIII_EW` | 121,092 | 0.028490 | 164.122 | 45.051 | 0.724551 |
| SGC | z2p1_3p5 | `LOG_CIV_MGII2796_EW` | 64,977 | 0.062415 | 118.655 | 55.805 | 0.780439 |
| SGC | z2p1_3p5 | `LOG_CIII_MGII2796_EW` | 64,809 | 0.060206 | 129.319 | 59.561 | 0.886228 |
| NGC | z2p1_3p5 | `LOG_CIV_MGII2796_EW` | 121,109 | 0.030251 | 294.353 | -75.820 | 0.916168 |

Minimum stability p-value:

- `p_min = 0.7245508982035929`

The stability suite therefore also returns a null-compatible result. The SGC high-z ratio axes are somewhat geometrically close, but their block-null p-values are high; by the preregistered criteria this is not a candidate.

## Interpretation

The preregistered QSO line-ratio family does not reveal a directional gradient.

This is a stronger negative result than the raw line-EW test in one important sense: line ratios are less sensitive to broad flux-scale and continuum-amplitude effects, yet the block-null p-values remain very high.

The current observational status remains:

- no robust QSO density dipole,
- no robust QSO raw emission-line residual dipole,
- no robust QSO line-ratio residual dipole,
- no robust LRG DN4000 residual dipole in the production bin already tested.

## Artifacts

- preregistration: `outputs/reports/qso_line_ratio_preregistration.md`
- result index: `outputs/tables/qso_line_ratio_preregistered_results.csv`
- ratio VAC cache: `data/interim/qso_highz_1p5_3p5_fastspecfit_line_ratio_vac.parquet`
- per-run CSVs: `outputs/tables/qso_line_ratio_primary_*_gradient.csv`, `outputs/tables/qso_line_ratio_stability_*_gradient.csv`
- per-run reports: `outputs/reports/qso_line_ratio_primary_*_gradient.md`, `outputs/reports/qso_line_ratio_stability_*_gradient.md`

## Final Status

Active null.

No line-ratio candidate is present in the preregistered DESI DR1 QSO high-z family.
