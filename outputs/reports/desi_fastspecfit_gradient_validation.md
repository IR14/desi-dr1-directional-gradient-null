# DESI FastSpecFit gradient validation

This is an observational validation report. It does not introduce new analytic constants.

## Inputs

- LSS catalog: `/Users/i.mikhailov/Desktop/work/cosmo/cosmo_genesis_gradient/data/raw/LRG_NGC_clustering.dat.fits`
- VAC/population catalog: `/Users/i.mikhailov/Desktop/work/cosmo/cosmo_genesis_gradient/data/raw/vac/fastspecfit/iron/v2.1/catalogs/fastspec-iron-main-dark.fits`
- random catalogs: 1
- redshift range: `0.4` to `0.6`

## Sample

- joined rows on TARGETID: 342791
- finite residual rows: 342791
- observable: `DN4000_MODEL`
- controls: `z; z2; LOGMSTAR`

## Dipole Fit

- amplitude: 0.0752201
- axis RA: 247.056 deg
- axis DEC: 38.150 deg
- fitted pixels: 648
- block-null p-value: 0.4091816367265469
- block-null mocks: 500

## Quality Cuts

| quality_cuts   |   n_input |   n_fail_zwarn |   n_fail_rchi2_cont |   n_fail_deltachi2 |   n_fail_dn4000_ivar |   n_fail_observable_finite |   n_after |   n_removed | winsorized_column   |   winsor_lower |   winsor_upper |
|:---------------|----------:|---------------:|--------------------:|-------------------:|---------------------:|---------------------------:|----------:|------------:|:--------------------|---------------:|---------------:|
| enabled        |    346759 |              9 |                 327 |               1331 |                 2301 |                          0 |    342791 |        3968 | DN4000_MODEL        |        1.23503 |        2.24397 |

## Residual Model Coefficients

| term      |   coefficient |
|:----------|--------------:|
| intercept |     1.71704   |
| z         |     0.369112  |
| z2        |    -0.398375  |
| LOGMSTAR  |    -0.0892507 |

## Figures

- `outputs/figures/desi_fastspecfit_gradient_validation_residual_vs_z.png`
- `outputs/figures/desi_fastspecfit_gradient_validation_residual_hist.png`

## Caveats

- This first local run fits a population-residual dipole only.
- Mock-calibrated p-values require rerunning the same estimator on the EZmock ensemble.
- A scientifically interpretable result requires stability across tracers, redshift bins, and systematics templates.
