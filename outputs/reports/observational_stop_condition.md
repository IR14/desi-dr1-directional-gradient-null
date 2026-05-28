# Observational stop condition

Created: 2026-05-28

Status: DESI DR1 observational search is stopped under the current data and protocol.

This document records a scientific stop condition for the current project phase. It is intended to prevent uncontrolled data dredging after repeated null results.

## Scope

The stop condition applies to the current DESI DR1 observational gradient program in this repository, using:

- DESI DR1 LSS clustering catalogs,
- DESI DR1 random catalogs,
- DESI DR1 FastSpecFit Iron VAC,
- current HEALPix dipole estimator,
- current spatial block-null tests,
- current external systematics templates,
- current preregistered QSO line-ratio family.

It does not claim that all possible anisotropy tests in cosmology are exhausted.

## Completed Test Families

The following families are closed for DESI DR1 unless reopened by a new preregistered protocol and a clearly justified new observable or calibration source:

| family | status | primary report |
|:--|:--|:--|
| LRG `DN4000_MODEL` population residuals | active null | `outputs/reports/desi_fastspecfit_gradient_validation.md` |
| QSO high-z density with random catalogs and external templates | active null | `outputs/reports/qso_highz_forge_density_followup.md` |
| QSO high-z raw emission-line residuals | active null | `outputs/reports/qso_highz_line_residual_summary.md` |
| QSO high-z emission-line region/bin stability | active null | `outputs/reports/qso_highz_line_region_bin_stability.md` |
| QSO preregistered line-ratio residuals | active null | `outputs/reports/qso_line_ratio_preregistered_results.md` |
| Master observational family with look-elsewhere accounting | active null | `outputs/reports/observational_gradient_master_null_report.md` |

## Stop Rule

Further searches on the same DESI DR1 data are stopped if they meet any of the following conditions:

- They reuse the same observables with only cosmetic changes to cuts, binning, or plotting.
- They add additional observables after seeing previous null results without preregistration.
- They interpret a single low p-value without family-level look-elsewhere accounting.
- They use QSO `DN4000_MODEL` as a high-z physical observable despite the documented survival of only 90 rows under strict quality cuts.
- They bypass random catalogs, survey masks, or systematics templates for density-like claims.

Under this stop rule, the current observational conclusion is:

> No robust empirical directional gradient has been detected in the completed DESI DR1 LSS + FastSpecFit checks.

## Reopen Conditions

The observational search may be reopened only if at least one of the following is true:

- DESI DR2/DR3 LSS catalogs or VACs are added.
- Official mocks become available for the exact property/residual estimator being tested.
- A new physical observable family is preregistered before execution, with fixed cuts, bins, controls, null tests, and candidate criteria.
- A methodological bug is found that invalidates an existing result; the bug and rerun protocol must be documented before rerunning.
- A new external systematic template set materially changes the correction model; the template set must be documented before execution.

## Required Protocol for Any Reopen

Before running a reopened family, create a preregistration report under `outputs/reports/` containing:

- exact observables,
- exact redshift bins,
- target tracers and regions,
- hard quality cuts,
- residual controls,
- map resolution,
- random catalogs and masks,
- null-test method and number of mocks,
- primary p-value,
- look-elsewhere family size,
- candidate and null criteria.

Then execute only the frozen family. Do not add extra observables mid-run.

## Final DESI DR1 Status

The DESI DR1 observational phase is closed as an active null.

This is a meaningful negative result: the pipeline was pushed through density, stellar-population, QSO emission-line, line-ratio, redshift-bin, and region-split checks without producing a robust repeated directional axis.

The next clean project phase is not more DR1 scanning. It is either:

- publication-style negative-result documentation,
- DESI DR2/DR3 readiness work,
- or independent theoretical/model work kept separate from the frozen observational artifacts.
