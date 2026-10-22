# Detection Engineering

> [!CAUTION]
> **Lab-developed content — tune before production use.**
> All detection logic in this repository was developed and tested in a lab environment.
> Before deploying, alter and tune each rule/query to match your own infrastructure — index names,
> data sources/log source types, field names and SIEM attributes/parsers — and baseline thresholds
> (e.g. byte sizes, counts) against your environment to avoid false positives or missed detections.
> Provided as-is, for defensive use only, without warranty.

SIEM detection content managed as code. Rules are written in [Sigma](https://github.com/SigmaHQ/sigma) as the single source of truth, mapped to MITRE ATT&CK, validated in CI, and converted to backend queries (Splunk SPL, Microsoft Sentinel KQL, Elastic).

## Repository layout

```
rules/
  windows/      Endpoint / Windows event & Sysmon detections
  linux/        Linux auditd / syslog detections
  network/      Firewall, proxy, IDS/IPS, DNS detections
  cloud/        AWS / Azure / M365 / GCP detections
  web/          Web server / WAF / proxy detections
detections/     Per-threat packs: write-up + native SIEM queries (QRadar, ArcSight, Sentinel, Cortex XDR)
templates/      Rule template to copy for new detections
tests/          Sample events / test cases per rule
docs/           Detection lifecycle, naming and contribution guide
.github/        CI workflow (Sigma lint + conversion) and PR template
```

## Threat detection packs

| Threat | Severity | Pack |
|---|---|---|
| CVE-2026-109618 / CVE-2026-109619 — PHP2Shell (PHP unauthenticated RCE) | Critical (CVSS 9.2) | [detections/CVE-2026-109618-php2shell](detections/CVE-2026-109618-php2shell/) |

## Rule lifecycle

`experimental` → `test` → `stable` → `deprecated`

1. Copy `templates/sigma_rule_template.yml` into the right `rules/<domain>/` folder.
2. Fill in logic, ATT&CK tags, false positives and level.
3. Add a sample event or test notes under `tests/`.
4. Open a pull request — CI validates the rule and converts it to Splunk SPL.
5. After tuning in production, promote `status` to `stable`.

## Local usage

```bash
pip install sigma-cli
sigma plugin install splunk
sigma check rules/
sigma convert -t splunk -p splunk_windows rules/windows/
```

## Naming convention

`<category>_<product>_<short_description>.yml`
e.g. `proc_creation_win_powershell_encoded_command.yml`

## License

Detection rules: [Detection Rule License (DRL) 1.1](https://github.com/SigmaHQ/Detection-Rule-License) recommended.
