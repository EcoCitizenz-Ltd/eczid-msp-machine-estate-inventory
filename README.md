# ECZ-ID MSP Machine Estate Inventory

Discover machine actors and machine-consumed surfaces in a customer repository, create a neutral evidence inventory, and identify the next review step.

This is a thin GitHub Marketplace discovery wrapper over the already-tested ECZ-ID MSP engine. It delegates to immutable engine commit `fedb5cb7633e7cf74c952291a7fbe302e5333af6`; it does not duplicate the engine or create a second source of truth.

## Quick start

```yaml
- uses: EcoCitizenz-Ltd/eczid-msp-machine-estate-inventory@v1
```

## Inputs

| Input | Required | Default | Meaning |
|---|---:|---|---|
| `path` | no | `.` | Repository-relative path to inspect. |
| `client-id` | no | empty | Optional MSP/customer identifier recorded locally; never sent to ECZ-ID. |
| `output` | no | `eczid-msp-machine-estate.json` | Repository-relative JSON report path. |
| `fail-on` | no | `invalid` | invalid or never. Missing ECZ-ID identity never fails the run. |

## Outputs

| Output | Meaning |
|---|---|
| `result-state` | NO_MACHINE_SURFACES, MACHINE_ESTATE_OBSERVED, REVIEW_RECOMMENDED, or INVALID_INPUT. |
| `machine-count` | Number of machine or machine-consumed surfaces observed. |
| `category-count` | Number of distinct observed categories. |
| `identity-reference-count` | Number of ECZ-ID or Resolver identity references observed. |
| `baseline-hash` | SHA-256 hash of the normalized inventory payload. |
| `report-path` | Path to the generated JSON report. |
| `next-action-url` | One contextual ECZ-ID next step, or empty when none is warranted. |

## Trust boundary

- Runs in the caller's GitHub Actions workspace.
- No repository source upload to ECZ-ID.
- No hidden telemetry.
- Missing ECZ-ID identity is neutral and never means unsafe, non-compliant or untrusted.
- No universal safety, trust, certification or compliance verdict.
- No pay-to-pass.
- Local MSP/customer policy decides what observed evidence means.

## Engine provenance

Delegates to `EcoCitizenz-Ltd/eczid-msp-machine-trust-toolkit@fedb5cb7633e7cf74c952291a7fbe302e5333af6`. Marketplace wrapper releases must only advance this pin after the shared engine's cross-platform tests are green.

## Version pinning

Use `@v1` for ECZ-ID's stable compatibility channel. Where your organisation requires immutable third-party Action references, pin the wrapper repository to its full release commit SHA. The wrapper itself always pins the shared MSP engine by full commit SHA.

## Support and policy

See [PRIVACY.md](PRIVACY.md), [SECURITY.md](SECURITY.md), [SUPPORT.md](SUPPORT.md) and [LICENSE.txt](LICENSE.txt).

## Why this wrapper exists

GitHub Marketplace discovery works at the repository root. The underlying MSP engine intentionally keeps related Actions together; this wrapper makes one proven capability independently discoverable without copying implementation or creating maintenance drift.
