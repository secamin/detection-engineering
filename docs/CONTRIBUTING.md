# Contributing Detections

## Workflow
1. Branch from `main`: `detection/<short-name>`
2. Add rule from the template; one rule per file.
3. Add test data under `tests/<rule-file-name>/` (sample log, expected result).
4. Open a PR using the template; CI must pass.
5. Peer review by a second detection engineer before merge.

## Severity guide
| Level | Meaning |
|---|---|
| critical | High-fidelity, confirmed malicious; page on-call |
| high | Likely malicious; triage within 1h |
| medium | Suspicious; triage same shift |
| low | Hunting / context; review in batches |
| informational | Enrichment only, no alert |

## Status guide
- **experimental** – new, not yet tuned
- **test** – deployed in SIEM, under tuning
- **stable** – tuned, low FP rate, production alerting
- **deprecated** – retired (keep for history)
