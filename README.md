# Multi-Source SOC Investigation: Web & SSH Attack Correlation

> Portfolio project based on a real security event observed in an authorised LearnCyber security environment.

## Overview
This case study documents a multi-source SOC investigation involving:
- repeated SSH authentication failures against a privileged account
- a Cloudflare-blocked request for `/wp-config.php-backup`
- Wazuh SIEM alerting and investigation
- threat-intelligence enrichment
- firewall containment
- MITRE ATT&CK mapping

The core skill demonstrated is **cross-source correlation**: starting with one alert and validating it against independent telemetry.

## Public-repository note
This is a sanitised portfolio version. Actual source IPs, internal hostnames, private URLs, screenshots and infrastructure identifiers have been removed or anonymised.

The original investigation was performed against infrastructure controlled by LearnCyber and was authorised.

**Attribution warning:** a shared IP range or subnet is an investigation lead, not proof that one threat actor controlled every address in that range.

## Objectives
1. Triage a Wazuh authentication alert.
2. Validate the alert against Linux authentication logs.
3. Identify password-guessing behaviour.
4. Enrich indicators with OSINT/threat intelligence.
5. Analyse Cloudflare security telemetry.
6. Correlate web and host-level activity.
7. Map observed behaviour to MITRE ATT&CK.
8. Determine whether compromise occurred.
9. Recommend containment and hardening.
10. Produce a professional incident report.

## Environment
| Component | Purpose |
|---|---|
| Wazuh | SIEM, alerting and event investigation |
| Linux/OpenSSH | Host and authentication telemetry |
| Cloudflare WAF | Web-layer security and blocking |
| UFW | Host firewall and containment |
| AbuseIPDB | IP reputation |
| VirusTotal | Threat intelligence |
| Shodan | Internet-facing service/context research |
| GreyNoise | Scanner/context research |
| MITRE ATT&CK | Behaviour mapping |

## Incident summary
Wazuh identified repeated failed SSH authentication attempts against `root` from an external source. Raw `auth.log` evidence confirmed repeated failed password attempts followed by pre-authentication connection closure.

A separate Cloudflare event showed another source in the same `/24` range probing `/wp-config.php-backup`; Cloudflare blocked the request.

Threat intelligence returned high abuse-confidence scores for the investigated addresses at the time of review. Firewall containment was then applied.

The reviewed evidence supports a **true-positive malicious SSH activity classification with no confirmed compromise**. The evidence does not, by itself, prove common threat-actor ownership of the observed subnet.

## Investigation workflow
**Alert triage → raw log validation → timeline → threat intelligence → Cloudflare correlation → MITRE mapping → containment → validation → reporting**

## Example authorised investigation commands
```bash
sudo grep "<REDACTED_IP>" /var/log/auth.log | wc -l
sudo grep "<REDACTED_IP>" /var/log/auth.log | tail -20
sudo grep "<REDACTED_SUBNET_PREFIX>" /var/log/auth.log
```

Only run these against systems and targets you own or have explicit permission to investigate.

## Key findings
- Repeated SSH password authentication failures targeted `root`.
- Reviewed attempts failed; no successful authentication was identified in the available evidence.
- Cloudflare blocked a suspicious request for `/wp-config.php-backup`.
- Additional activity was observed from another address in the same `/24`.
- Threat intelligence provided supporting context.
- Firewall containment was implemented.
- MITRE mapping was performed conservatively, separating confirmed behaviour from hypotheses.

## Repository contents
- [`incident-report.md`](incident-report.md) - full investigation report
- [`timeline.csv`](timeline.csv) - investigation timeline
- [`mitre-mapping.md`](mitre-mapping.md) - ATT&CK assessment
- [`remediation.md`](remediation.md) - containment and improvement plan
- [`analyst-notes.md`](analyst-notes.md) - reasoning and investigation prompts
- [`portfolio-summary.md`](portfolio-summary.md) - CV/interview-ready wording
- `evidence/` - sanitised evidence only

## Portfolio lesson
A strong analyst does not simply identify malicious activity. They explain:
**what happened, what proves it, what is only suspected, what was done, and what remains unknown.**

## Author
**Daniel Oseghale**  
Cybersecurity | Security Operations | Threat Intelligence | Cybersecurity Education

## Disclaimer
All security activity described here was conducted against authorised infrastructure. Never scan, exploit or access third-party systems without explicit permission.
