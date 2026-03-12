# Extraction Specification — RH Canonical Lane

## Objective

Put the RH constants surface on the same explicit extraction pipeline used by the
other canonical-lane repos without replacing the native RH drift guard.

## Pipeline

```text
  constants_extraction_inputs.json
            |
            v
  [1] extract_constants.py
            |
            v
  constants_extracted.json        (validated intermediate)
            |
            v
  [2] promote_constants.py
            |
            +---> constants_registry.json   (updated)
            +---> stitch_constants.json     (updated)
            +---> promotion_report.json     (audit trail)
            |
            v
  [3] rh_closure_drift_guard.py
            |
            v
  certificate_runtime.json        (native RH gate evaluation)
```

The extraction/promote layer standardizes provenance. The drift guard remains the
single source of truth for RH gate status.

## Main Constants

| Name | Formula | Constraint | Source section |
|---|---|---|---|
| `xi_tail` | `xi_tail_raw` | nonnegative | `13.43/13.53M theorem extraction (canonical branch formulas)` |
| `c_r` | `c_r_raw` | nonnegative | `13.53P.8 theorem extraction (canonical branch constants)` |
| `rho_nf` | `rho_nf_raw` | positive | `13.53P.8 theorem extraction (canonical branch constants)` |
| `delta_rec` | `delta_rec_raw` | positive | `13.53P.8 theorem extraction (canonical branch constants)` |
| `eps_coh` | `eps_coh_raw` | nonnegative, strict zero | `13.53P.8.3 strict canonical normalization` |
| `mu_strat` | `mu_strat_raw` | positive | `13.43/13.53M theorem extraction (canonical branch formulas)` |

## Stitch Constants

| Name | Formula | Constraint | Source section |
|---|---|---|---|
| `l_d_can` | `l_d_can_raw` | positive | `13.47 + 13.53N.2` |
| `sigma_star_can` | `sigma_star_can_raw` | positive | `13.47 + 13.53N.2` |
| `eta_coh_star_can` | `eta_coh_star_can_raw` | nonnegative, strict zero | `13.53P.8.3 + 13.53N.2` |

## Validation Rules

- `required_positive`: normalized value must be `> 0`.
- `required_nonnegative`: normalized value must be `>= 0`.
- `strict_zero`: normalized value must equal `0.0` to machine tolerance.

All RH references are currently `1.0`, so raw and promoted values coincide.

## Output Artifacts

| File | Producer | Consumer |
|---|---|---|
| `artifacts/constants_extracted.json` | `extract_constants.py` | `promote_constants.py` |
| `artifacts/constants_registry.json` | `promote_constants.py` | `rh_closure_drift_guard.py` |
| `artifacts/stitch_constants.json` | `promote_constants.py` | `rh_closure_drift_guard.py` |
| `artifacts/promotion_report.json` | `promote_constants.py` | audit / reviewer surface |
| `repro/certificate_runtime.json` | `rh_closure_drift_guard.py` | rerun protocol |

## Provenance Rule

The RH repo keeps its native drift-guard evaluation, but the registry and stitch
files must now be produced from `constants_extraction_inputs.json` via the
standard extract/promote path before guard execution.
