# MITRE ATT&CK Coverage

| Tactic | Technique | Rule | Status |
|---|---|---|---|
| Execution / Defense Evasion | T1059.001, T1027 | rules/windows/proc_creation_win_powershell_encoded_command.yml | experimental |
| Initial Access | T1190 | rules/web/web_cve_2026_109618_php2shell_exploit_attempt.yml (CVE-2026-109618) | test |
| Initial Access | T1190 | rules/web/web_cve_2026_109618_php2shell_upload_progress_body.yml (CVE-2026-109618) | experimental |
| Execution / Discovery | T1190, T1082 | rules/web/web_cve_2026_109618_php2shell_success_marker.yml (CVE-2026-109618) | experimental |

Tip: generate an ATT&CK Navigator layer from rule tags with `sigma2attack` (from pySigma tooling) and import it at https://mitre-attack.github.io/attack-navigator/.
