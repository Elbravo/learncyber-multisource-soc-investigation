# Analyst Notes

## Questions
### Triage
- What triggered the alert?
- What asset was targeted?
- What account was targeted?
- Was authentication successful?
- How often did the source connect?

### Correlation
- Are there related Cloudflare events?
- Are there related Wazuh alerts?
- Are other IPs from the same ASN/range active?
- Are timestamps aligned?
- Are request patterns similar?

### Threat intelligence
- Is the source known for scanning?
- Is the reputation current?
- What ASN owns it?
- Is it hosting, VPN, proxy or residential infrastructure?
- Does external reputation agree with local evidence?

## Attribution discipline
Do not conclude that a whole subnet belongs to one attacker merely because multiple IPs appear in the same range.

Prefer:
> Multiple related indicators were observed within the same network range. This justified further threat hunting but did not independently establish common ownership or attribution.

## Confidence model
**High:** directly supported by local telemetry.  
**Medium:** multiple supporting indicators, but alternatives remain.  
**Low:** plausible hypothesis requiring more evidence.

## Portfolio lesson
Professional SOC work includes knowing when the evidence is insufficient.
