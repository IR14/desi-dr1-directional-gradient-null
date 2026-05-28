# QSO high-z forge density follow-up

Created: 2026-05-27

This follow-up responds to the FastSpecFit QSO high-z population run, where
`DN4000_MODEL` was not a useful quasar observable after strict quality cuts
(`518736 -> 90` usable rows). The scientifically relevant next test is therefore
a QSO sky-density dipole using DESI LSS clustering catalogs and random catalogs.

## Inputs

- tracer: QSO
- regions: NGC+SGC
- redshift bins: `1.5 <= z < 2.1`, `2.1 <= z <= 3.5`
- map resolution: HEALPix `nside=16`
- density correction: DESI random catalogs
- weights: DESI catalog weights
- null tests: 5000 pixel permutations, 5000 block-null mocks
- block regions: 48
- external templates: EBV, stellar density, galdepth g/r/z, psfsize g/r/z, COSKY g/r/z

## Combined NGC+SGC Density + External Templates

| z_min | z_max | n_data | raw_amp | raw_axis_ra | raw_axis_dec | raw_perm_p | raw_block_p | corrected_amp | corrected_axis_ra | corrected_axis_dec | corrected_perm_p | corrected_block_p |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 1.5 | 2.1 | 432458 | 0.003784 | 46.946 | 51.756 | 0.991602 | 0.834633 | 0.003703 | 87.961 | -78.002 | 0.992801 | 0.840432 |
| 2.1 | 3.5 | 366560 | 0.008607 | 324.673 | 15.966 | 0.851230 | 0.240952 | 0.003987 | 329.996 | -4.010 | 0.980404 | 0.780044 |

The only mildly lower diagnostic value is the raw block-null p-value in
`2.1 <= z <= 3.5` (`p=0.241`), but after external-template regression the
amplitude drops by more than a factor of two and the block-null p-value rises
to `0.780`. This is not evidence for a directional signal.

## Region Split

| region | z_min | z_max | n_data | amplitude | axis_ra | axis_dec | perm_p | poisson_p | block_p |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| NGC | 1.5 | 2.1 | 281438 | 0.009911 | 120.968 | 80.962 | 0.977005 | 0.528694 | 0.653069 |
| NGC | 2.1 | 3.5 | 237306 | 0.006319 | 339.286 | 44.405 | 0.985203 | 0.840032 | 0.876625 |
| SGC | 1.5 | 2.1 | 151020 | 0.018968 | 187.966 | -54.340 | 0.978804 | 0.514097 | 0.765847 |
| SGC | 2.1 | 3.5 | 129254 | 0.017125 | 263.096 | -0.890 | 0.970006 | 0.630874 | 0.787043 |

The cap-split axes are not coherent, and all p-values remain comfortably
compatible with the isotropic null.

## Artifacts

- `outputs/tables/qso_highz_density_external_templates_summary.csv`
- `outputs/reports/qso_highz_density_external_templates_summary.md`
- `outputs/tables/qso_highz_density_region_split.csv`
- `outputs/reports/qso_highz_density_region_split_summary.md`
- `outputs/reports/desi_qso_highz_forge_validation.md`

## Scientific Status

Phase 3 QSO high-z density follow-up returns an active null result. The data do
not support a stable high-redshift QSO directional density axis under the
current random-catalog correction, external-template regression, and cap-split
sanity checks.

The best next observational target is not QSO `DN4000_MODEL`; it is either:

- pure QSO density with official mock calibration for the exact high-z selection, or
- emission-line/QSO-specific VAC observables if a suitable column set is available.
