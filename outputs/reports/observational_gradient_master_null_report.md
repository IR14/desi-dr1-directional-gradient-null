# Observational gradient master null report

Created: 2026-05-28

Status: active null across the current DESI DR1 observational gradient test family.

This report consolidates the completed DESI DR1 checks for a directional sky-gradient signal. It does not introduce new formulas or tune model constants. The question tested here is narrower and empirical:

> After survey geometry, random catalogs, quality cuts, line/population residualization, and external imaging templates where applicable, do the tested observables show a statistically robust dipole/axis?

The answer for the current test family is no.

## Included Test Family

The master family contains 17 controlled block-null tests:

- 1 LRG population-residual test: `DN4000_MODEL`, `0.4 <= z < 0.6`, NGC.
- 2 QSO high-z combined density tests after external-template correction.
- 4 QSO high-z density region-split tests.
- 2 QSO high-z emission-line residual tests, combined NGC+SGC.
- 8 QSO high-z emission-line residual tests split by NGC/SGC and redshift bin.

The QSO `DN4000_MODEL` high-z smoke run is recorded as a diagnostic artifact but excluded from the primary family because only 90 QSO rows survived the DN4000 quality cuts.

Machine-readable index:

- `outputs/tables/observational_gradient_master_null_tests.csv`

## Look-Elsewhere Accounting

Primary family size: `m = 17`

Minimum block-null p-value in the primary family:

- `p_min = 0.4091816367`
- test: `lrg_dn4000_model_z0p4_0p6`

Simple global corrections:

| correction | value | interpretation |
|:--|--:|:--|
| Bonferroni `min(1, m * p_min)` | 1.000000 | no post-trial anomaly |
| Sidak `1 - (1 - p_min)^m` | 0.999870 | such a p-minimum is entirely common under H0 |

Including the excluded QSO DN4000 smoke diagnostic changes neither conclusion nor `p_min`:

- `m = 18`
- `p_min = 0.4091816367`
- Bonferroni-adjusted value: `1.000000`
- Sidak global value: `0.999923`

Even if the raw, pre-template QSO density diagnostic value `p=0.2409518` is included as a stress check, the family still has no look-elsewhere concern:

- Bonferroni-adjusted value: `1.000000`
- Sidak global value for `m=18`: `0.993004`

## Result Summary

| family | tests | minimum block-null p-value | status |
|:--|--:|--:|:--|
| LRG population residual | 1 | 0.409182 | null-compatible |
| QSO density corrected combined | 2 | 0.780044 | null-compatible |
| QSO density region split | 4 | 0.653069 | null-compatible |
| QSO line residual combined | 2 | 0.904192 | null-compatible |
| QSO line residual region/bin | 8 | 0.816367 | null-compatible |

No test in the controlled family approaches a discovery-like or even candidate-like threshold. The result is not a weak detection after correction; it is an absence of low-p events.

## Key Observational Runs

### LRG DN4000_MODEL

- report: `outputs/reports/desi_fastspecfit_gradient_validation.md`
- tracer/region: LRG NGC
- redshift: `0.4 <= z < 0.6`
- rows after quality cuts: 342,791
- amplitude: 0.0752201
- axis: RA 247.056 deg, DEC 38.150 deg
- block-null p-value: 0.4091816367

Interpretation: no statistically significant DN4000 residual dipole in the tested mature LRG sample.

### QSO High-z Density

- report: `outputs/reports/qso_highz_forge_density_followup.md`
- tracer/regions: QSO NGC+SGC plus NGC/SGC splits
- redshift bins: `1.5 <= z < 2.1`, `2.1 <= z < 3.5`
- correction: random catalogs and external templates for EBV, stellar density, depth, seeing, and sky brightness

Combined corrected tests:

| z range | n_data | corrected amplitude | axis RA deg | axis DEC deg | corrected block p |
|:--|--:|--:|--:|--:|--:|
| 1.5-2.1 | 432,458 | 0.003703 | 87.961 | -78.002 | 0.840432 |
| 2.1-3.5 | 366,560 | 0.003987 | 329.996 | -4.010 | 0.780044 |

Region-split block p-values are also high: 0.653, 0.877, 0.766, and 0.787. Axes are not coherent across NGC/SGC.

Interpretation: no robust high-z QSO density axis after random-catalog and external-template correction.

### QSO High-z Emission Lines

- combined report: `outputs/reports/qso_highz_line_residual_summary.md`
- region/bin report: `outputs/reports/qso_highz_line_region_bin_stability.md`
- VAC cache: `data/interim/qso_highz_1p5_3p5_fastspecfit_line_vac.parquet`
- observables: `CIV_1549_EW`, `CIII_1908_EW`
- redshift: `1.5 <= z < 3.5`
- controls: `z`, `z^2`, `LOGMSTAR`, QSO line-fit diagnostics, luminosity proxies, and external imaging templates

Combined tests:

| observable | rows | amplitude | axis RA deg | axis DEC deg | block p |
|:--|--:|--:|--:|--:|--:|
| `CIV_1549_EW` | 761,395 | 0.303061 | 85.281 | 7.464 | 0.958084 |
| `CIII_1908_EW` | 758,337 | 0.148250 | 132.129 | -42.987 | 0.904192 |

The combined CIV/CIII axes are separated by 65.953 degrees.

Region/bin split:

| region | z range | observable | rows | amplitude | block p |
|:--|:--|:--|--:|--:|--:|
| NGC | 1.5-2.1 | `CIV_1549_EW` | 266,722 | 0.831954 | 0.816367 |
| NGC | 1.5-2.1 | `CIII_1908_EW` | 264,221 | 0.129588 | 0.972056 |
| NGC | 2.1-3.5 | `CIV_1549_EW` | 228,136 | 0.452652 | 0.954092 |
| NGC | 2.1-3.5 | `CIII_1908_EW` | 228,933 | 0.207706 | 0.942116 |
| SGC | 1.5-2.1 | `CIV_1549_EW` | 142,895 | 0.625780 | 0.988024 |
| SGC | 1.5-2.1 | `CIII_1908_EW` | 141,485 | 0.087681 | 0.996008 |
| SGC | 2.1-3.5 | `CIV_1549_EW` | 123,642 | 0.541443 | 0.990020 |
| SGC | 2.1-3.5 | `CIII_1908_EW` | 123,698 | 0.267788 | 0.966068 |

Interpretation: no line-residual test gives a low block-null p-value. The one relatively close axis pair, SGC `2.1-3.5`, has p-values 0.990 and 0.966, so it is not an anomaly.

## Scientific Interpretation

The current DESI DR1 observational program does not detect a stable directional gradient.

More precisely:

- H0 is retained: the tested data are compatible with isotropy after the implemented corrections.
- H1 is not supported by this test family: there is no repeated low-p axis across tracer, redshift, region, density, DN4000, or QSO line residual checks.
- This is not a proof that no anisotropy exists anywhere; it is a negative result for the specific DESI DR1 observables, cuts, masks, random catalogs, templates, and null procedures used here.

The most important methodological result is that the pipeline did not manufacture a signal when pushed into multiple natural follow-up branches.

## Known Limitations

- The LRG population test currently covers one production interval, `0.4 <= z < 0.6`, in NGC.
- QSO `DN4000_MODEL` is not a useful high-z QSO observable under the strict FastSpecFit quality cuts; only 90 rows survived in the smoke run.
- QSO line residual tests use block shuffling, not official QSO-specific EZmock line-property mocks.
- Density tests are stronger for survey geometry because they use DESI random catalogs directly; population/line residual tests still depend on the residual model and external template coverage.
- The p-values are correlated across related splits, so Bonferroni/Sidak are used only as simple sanity checks. Since all p-values are high, this does not affect the conclusion.

## Final Status

Active null.

No robust empirical directional gradient has been found in the completed DESI DR1 observational checks.

The next scientifically clean move, if the project continues, is to pre-register a new observable family before running it. The best candidate is QSO line ratios such as `CIV/CIII` or `CIV/MGII`, because ratios can suppress broad calibration and luminosity effects better than raw equivalent widths.
