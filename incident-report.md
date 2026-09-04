# Incident Investigation Report

## Incident
**Multi-Source Web and SSH Attack Correlation**

## Classification
- Type: Malicious external activity
- Primary behaviour: SSH password guessing
- Status: Contained
- Impact: No confirmed compromise in reviewed evidence
- Confidence: High for malicious SSH activity; medium for broader coordination hypothesis

## Executive summary
A Wazuh alert identified repeated failed SSH authentication attempts against a privileged account on a security monitoring host.

Linux authentication logs confirmed repeated failed password attempts followed by pre-authentication connection closure.

The investigation was expanded after Cloudflare telemetry showed a separate suspicious request for `/wp-config.php-backup` from another source in the same `/24` range. Cloudflare blocked the request.

Threat intelligence provided additional context, and firewall containment was applied.

No successful SSH authentication was identified in the reviewed evidence.

The shared network range was treated as a correlation lead rather than definitive proof of a single threat actor.

## Evidence assessment
| Evidence | Finding | Confidence |
|---|---|---|
| Wazuh | Authentication failure alert | High |
| Linux auth.log | Repeated failed SSH password attempts | High |
| SSH outcome | Reviewed attempts failed | High |
| Cloudflare | Suspicious request blocked | High |
| Threat intelligence | High abuse confidence at time of review | Medium/High |
| Shared `/24` | Multiple observed sources | Medium |
| Single threat actor attribution | Not established | Low |

## Findings

### 1. SSH password guessing
Repeated failed SSH password authentication attempts targeted `root`.

**Assessment:** True positive, high confidence.

### 2. Related network activity
Another source in the same `/24` was observed in SSH telemetry.

**Assessment:** Relevant for threat hunting, but insufficient by itself to prove common ownership or coordination.

### 3. Web-layer probing
Cloudflare blocked a request for `/wp-config.php-backup`.

**Assessment:** Suspicious and security-relevant. The available evidence does not establish successful file access or exploitation.

## MITRE ATT&CK
See [`mitre-mapping.md`](mitre-mapping.md).

Primary mapping:
- T1110.001 - Password Guessing

Conditional mappings:
- T1595 - Active Scanning
- T1190 - Exploit Public-Facing Application

These conditional mappings require supporting evidence and should not be overstated.

## Containment
- Confirmed malicious SSH source was blocked at the firewall.
- Broader network-range containment was applied during the investigation.
- Cloudflare had already blocked the web-layer request.

Subnet-wide blocking should always be assessed against business impact and false-positive risk.

## Recommendations
### Immediate
- Confirm no successful privileged authentication occurred.
- Review privileged command activity.
- Continue monitoring SSH telemetry.
- Validate firewall containment.

### Short term
- Disable direct root SSH login where appropriate.
- Prefer SSH key authentication.
- Restrict management access where feasible.
- Review Wazuh brute-force correlation thresholds.
- Correlate Cloudflare and host telemetry.

### Long term
- Develop documented SSH detection and response procedures.
- Improve cross-source correlation.
- Monitor slow-rate authentication attempts.
- Enrich high-value indicators with threat intelligence.
- Review internet-facing services regularly.

## Final verdict
**True positive: repeated malicious SSH password-guessing activity, with no confirmed compromise in the reviewed evidence.**

Additional web activity and shared network-range observations justified broader investigation but were not sufficient to prove single-actor attribution.
