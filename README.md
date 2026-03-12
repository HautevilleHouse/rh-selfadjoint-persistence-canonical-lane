# The Riemann Hypothesis via Self-Adjoint Spectral Persistence
## Canonical Lane (defined term): the manifold-constrained local-to-global closure architecture for the RH program.

Canonical Lane research workspace for the Millennium Problem:

the distribution of the nontrivial zeros of the Riemann zeta function on the critical line.

## Main Manuscript

- [paper/RH_SELF_ADJOINT_PERSISTENCE_PREPRINT.md](paper/RH_SELF_ADJOINT_PERSISTENCE_PREPRINT.md)
- [paper/CANONICAL_ROUTING_INDEX.md](paper/CANONICAL_ROUTING_INDEX.md)

## Structure

- `paper/`
  - `RH_SELF_ADJOINT_PERSISTENCE_PREPRINT.md`

- `notes/`
  - `EG1_public.md`
  - `EG2_public.md`
  - `EG3_public.md`
  - `EG4_public.md`
  - `IDENTIFICATION_BRIDGE.md`

- `repro/`
  - `REPRO_PACK.md`
  - `THIRD_PARTY_RERUN_PROTOCOL.md`
  - `run_repro.sh`
  - `repro_manifest.json`
  - `certificate_baseline.json`

- `scripts/`
  - `extract_constants.py`
  - `promote_constants.py`
  - `rh_closure_drift_guard.py`
  - `rh_closure_registry.py`
  - `rh_closure_target_calculator.py`
  - `extract_rh_e3_margin.py`
  - `rh_formalism_guard.py`
  - `update_manifest.py`
  - `verify_manifest.py`

- `artifacts/`
  - `constants_extraction_inputs.json`
  - `constants_extracted.json`
  - `constants_registry.json`
  - `stitch_constants.json`
  - `promotion_report.json`
 
## Local Repro Command

```bash
bash repro/run_repro.sh
```

This refreshes the extracted/pro promoted constants and writes `repro/certificate_runtime.json`.

## How To Read This Professionally

1. Theorem chain first: read `paper/RH_SELF_ADJOINT_PERSISTENCE_PREPRINT.md`.
2. Constants provenance second: audit `paper/EXTRACTION_SPEC.md`, `artifacts/constants_extraction_inputs.json`, `artifacts/constants_extracted.json`, `artifacts/constants_registry.json`, and `artifacts/stitch_constants.json`.
3. Pipeline third: run `bash repro/run_repro.sh` to audit hashes/provenance/gates; it is reproducibility infrastructure, not theorem generation.

Current RH runner policy:

- `repro/run_repro.sh` executes `extract -> promote -> native drift guard -> manifest verify`.
- `repro/run_repro.sh` executes `extract -> promote -> native drift guard -> manifest refresh -> manifest verify`.
- The RH drift guard remains the final gate evaluator; the extraction layer standardizes constants provenance without changing gate logic.

## Citation

- Metadata: [`CITATION.cff`](CITATION.cff).
- Manuscript target: [paper/RH_SELF_ADJOINT_PERSISTENCE_PREPRINT.md](paper/RH_SELF_ADJOINT_PERSISTENCE_PREPRINT.md)

## Authorship

- Program author: **HautevilleHouse**
- Canonical attribution source: [`CITATION.cff`](CITATION.cff)
