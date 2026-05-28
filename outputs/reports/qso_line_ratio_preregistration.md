# QSO line-ratio gradient preregistration

Created: 2026-05-28

Status: frozen before execution.

This document preregisters the next observational family after the DESI DR1 master null report. No result from this family is to be interpreted unless it matches the definitions below.

## Motivation

Raw QSO equivalent widths returned active null results. A line-ratio observable can suppress broad continuum calibration, luminosity scale, and some selection effects better than a raw line equivalent width. This family therefore tests whether relative high-ionization / lower-ionization line strength residuals show a sky dipole.

## Primary Observables

The primary observables are natural-log equivalent-width ratios:

1. `LOG_CIV_CIII_EW = ln(CIV_1549_EW / CIII_1908_EW)`
2. `LOG_CIV_MGII2796_EW = ln(CIV_1549_EW / MGII_2796_EW)`
3. `LOG_CIII_MGII2796_EW = ln(CIII_1908_EW / MGII_2796_EW)`

Only rows where both numerator and denominator are finite and strictly positive are eligible.

The propagated inverse-variance weight for `ln(x/y)` is:

`IVAR_ratio = 1 / (1 / (IVAR_x * x^2) + 1 / (IVAR_y * y^2))`

Rows with non-positive or non-finite propagated IVAR are excluded.

## Data and Sample

- LSS sample: DESI DR1 QSO clustering catalogs, NGC and SGC.
- VAC sample: DESI DR1 FastSpecFit Iron main dark.
- Redshift domain: `1.5 <= z < 3.5`.
- Regions: NGC+SGC combined for primary tests; NGC and SGC separately for stability.
- HEALPix resolution: `nside=16`.
- Minimum objects per fitted pixel: `10`.

## Redshift Bins

Primary bins:

1. `1.5 <= z < 2.1`
2. `2.1 <= z < 3.5`

The full `1.5 <= z < 3.5` combined run may be recorded as diagnostic context, but the preregistered primary family uses the two bins above.

## Quality Rules

Hard cuts:

- `ZWARN == 0`
- finite ratio value
- positive propagated ratio IVAR
- winsorization of each ratio at the 1st and 99th percentile after hard cuts

Line-fit diagnostics are not hard cuts for QSO line ratios because `DELTA_LINECHI2 > 25` was empirically shown to remove nearly the full high-z QSO sample for these VAC columns. Instead, the residual model includes:

- `RCHI2_LINE`
- `DELTA_LINECHI2`

## Residual Model Controls

For each eligible row, regress the ratio observable against:

- `z`
- `z^2`
- `LOGMSTAR`
- `RCHI2_LINE`
- `DELTA_LINECHI2`
- luminosity/photometry proxies available in the VAC cache:
  - `FLUX_SYNTH_G`, `FLUX_SYNTH_R`, `FLUX_SYNTH_Z`
  - `FLUX_G`, `FLUX_R`, `FLUX_Z`
  - `FLUX_W1`, `FLUX_W2`
- external imaging templates:
  - EBV
  - stellar density
  - g/r/z depth
  - g/r/z PSF size
  - g/r/z sky brightness

## Null Test

Use the existing spatial block permutation null:

- `block_null_mocks = 500`
- `block_nside = 2`
- random seed: `20260527`

The primary p-value is `block_null_p_value`.

## Test Family and Look-Elsewhere Rule

Primary family:

- 3 line ratios
- 2 redshift bins
- NGC+SGC combined

Primary test count: `m = 6`.

Stability suite:

- the same 3 line ratios
- the same 2 redshift bins
- NGC and SGC separately

Stability test count: `m = 12`.

Interpretation thresholds:

- `p >= 0.05`: null-compatible.
- `0.01 <= p < 0.05`: weak diagnostic only; not a candidate after look-elsewhere unless repeated across ratios/regions.
- `p < 0.01`: candidate only if the axis is stable across at least two ratios and at least one region split.
- Discovery-like language is forbidden for this family. At most, the result can be called a candidate requiring independent mocks and DR2 replication.

## Frozen Command Pattern

Every run must use:

- `cosmo-gradient fastspecfit-gradient`
- `--nside 16`
- `--min-objects-per-pixel 10`
- `--block-null-mocks 500`
- `--block-nside 2`
- `--seed 20260527`
- the same 11 external templates used in the QSO line residual tests.

No additional ratios or altered cuts are allowed in the first execution of this preregistered family.
