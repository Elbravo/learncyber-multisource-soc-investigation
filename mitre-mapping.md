# MITRE ATT&CK Mapping

| Tactic | Technique | Assessment | Evidence |
|---|---|---|---|
| Credential Access | T1110.001 - Password Guessing | High | Repeated failed SSH password authentication |
| Reconnaissance | T1595 - Active Scanning | Medium / conditional | Requires telemetry showing systematic scanning |
| Initial Access | T1190 - Exploit Public-Facing Application | Low / conditional | Suspicious web request; no confirmed exploitation |

## T1110.001 - Password Guessing
Repeated SSH password authentication failures against a privileged account are consistent with password-guessing activity.

**Confidence: High**

No successful authentication is claimed.

## T1595 - Active Scanning
Multiple suspicious sources were observed, including activity from the same `/24`.

**Confidence: Medium / conditional**

A shared network range is useful for hunting, but does not prove common ownership. Stronger evidence would include consistent scanning patterns, timing, fingerprints or additional network telemetry.

## T1190 - Exploit Public-Facing Application
Cloudflare blocked a request for `/wp-config.php-backup`.

**Confidence: Low / conditional**

The request is suspicious, but the available evidence does not establish successful exploitation. Retain this mapping only if further evidence demonstrates an exploitation attempt.

## Analyst principle
Map **observed behaviour**, not the most dramatic interpretation of an alert.
