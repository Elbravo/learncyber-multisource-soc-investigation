# Remediation and Detection Improvements

## Immediate
- Confirm whether privileged authentication succeeded.
- Review privileged command activity.
- Maintain containment for confirmed malicious sources.
- Monitor for recurrence.

## SSH hardening
- Disable direct root login where operationally appropriate.
- Prefer SSH keys.
- Restrict administrative access to trusted sources where feasible.
- Apply rate limiting/brute-force controls.
- Review exposed management services.

## Wazuh detection improvements
Develop correlation logic for:
- repeated failures from one source
- repeated failures against privileged accounts
- distributed failures across a network range
- successful login after repeated failures
- suspicious activity following authentication

## Cloudflare monitoring
Watch for:
- configuration/backup-file probing
- administrative path discovery
- unusual request rates
- repeated requests from related infrastructure
- WAF events correlated with host telemetry

## Cross-source correlation keys
- source IP
- timestamp
- ASN
- network range
- user agent
- destination
- request path
- destination port
- WAF rule
- IDS signature

## Post-containment validation
1. Verify the firewall rule.
2. Confirm new activity stops or changes.
3. Check for alternate source addresses.
4. Review successful authentication.
5. Review privileged command execution.
6. Check persistence indicators.
7. Record the final outcome.

## Risk note
Blocking an entire `/24` can reduce attack surface but may also block legitimate traffic. Use broader containment only when justified by evidence and operational context.
