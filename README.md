# Cloudora Triage Shift — Simulated SOC Engagement

**Type:** Simulated client engagement (fictional client, MyFirstHack training)  
**Role:** SOC Analyst (triage)  
**Scope:** 12 alerts, single shift, triaged and ticketed in ServiceNow  

## Summary

I ran a full alert triage queue for a fictional B2B HR software client (Cloudora),
covering identity, endpoint, network, and email-based alerts. Each alert was worked
to a written verdict: hypothesis stated in both directions, evidence checked against
context (change records, schedules, helpdesk tickets, sign-in history), and a final
call on verdict, severity, and action — defensible by another analyst without
re-doing the investigation.

**Result:** 2 true positives, 1 escalation, 7 false positives (root-caused), 1
held pending evidence, 1 duplicate closed.

## Triage Method

1. **Read the alert** — what the detection rule actually fires on, not just the headline.
2. **State the hypothesis both ways** — malicious and benign, before touching evidence.
3. **Check context first** — change records, maintenance windows, helpdesk tickets,
   known schedules. Most false positives resolve here.
4. **Pivot to raw evidence** — sign-in slices, AV logs, email headers — and baseline
   the entity (device fingerprint, IP, location, historical protocol use).
5. **Reach one of five verdicts** — True Positive, False Positive, Escalate,
   Insufficient Data, or Duplicate — with severity set from impact × confidence,
   and every claim tied to a named piece of evidence.

## Alert Index

| ID | Alert | Verdict | Severity | MITRE |
|---|---|---|---|---|
| CLD-0101 | Failed sign-ins on svc-backup | False Positive (change window) | Informational | — |
| CLD-0102 | Active credential stealer on LDN-WS-117 | **True Positive** | Sev 2 | T1204.002 |
| CLD-0103 | Internal port scanning | False Positive (authorized scanner) | Informational | — |
| CLD-0104 | Repeated MFA failures → success, nina.cole | False Positive (user error) | Informational | — |
| CLD-0105 | Suspicious payslip email | False Positive (legitimate, auth passed) | Informational | — |
| CLD-0106 | Automated digest: unresolved threat | Duplicate of CLD-0102 | Tracked on CLD-0102 | — |
| CLD-0107 | Mass file deletion from SharePoint | False Positive (retention automation) | Informational | — |
| CLD-0108 | Unfamiliar sign-in, gwen.muir | **True Positive** | Sev 2 | T1078.004 |
| CLD-0109 | Outbound beaconing, 3 hosts | **Escalated** | Sev 2 | T1071.001 (suspected) |
| CLD-0110 | Blocked sign-ins from watchlist IP | True Positive, no impact | Sev 4 | T1110.003 |
| CLD-0111 | Suspicious invoice email | Insufficient Data (on hold) | Sev 4 | T1566.001 (if confirmed) |
| CLD-0112 | Impossible travel, omar.farah | False Positive (token refresh) | Informational | — |

## Files

- `Cloudora_Triage_shift.pdf` - triage verdict worksheet covering all 12 alerts (CLD-0101–CLD-0112), each with alert detail, hypothesis, evidence checked, verdict, severity, action, justification, and MITRE mapping
