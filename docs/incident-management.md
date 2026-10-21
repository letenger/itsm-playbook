# Incident Management Procedure

Applies to: all unplanned interruptions or degradation of a university IT service, plus any event that threatens to cause one. Owner: Service Desk Manager. Aligned with ITIL 4 incident management.

## Definitions

- **Incident** — an unplanned interruption to a service, or a reduction in the quality of a service. The goal of incident management is to restore normal service as quickly as possible; root cause removal is problem management.
- **Major incident** — an incident with extensive impact requiring coordinated cross-team response and executive communication.
- **Service request** — a request for something already approved and catalogued (access, software, hardware). Log as a request, not an incident.

## Priority matrix

Priority is derived from impact × urgency. When in doubt, raise the priority; downgrading later is cheap, under-triaging is not.

| Priority | Impact (breadth and criticality) | Urgency | Examples | Response / resolution target |
| --- | --- | --- | --- | --- |
| P1 — Critical | Extensive: campus-wide service down, or a critical system (SIS, network, authentication) unavailable during teaching/exams | Immediate | Campus Wi-Fi outage during lectures; M365 authentication failure; SIS unavailable in enrolment period | 15 min / 4 hours (24×7) |
| P2 — High | Significant: a whole school or department affected, or a critical service degraded with no workaround | High | Lecture theatre AV failure during teaching; department printer farm down; VPN unusable | 30 min / 8 business hours |
| P3 — Moderate | Limited: an individual or small team affected, workaround available | Medium | Single laptop fault; one user's MFA reset; one shared mailbox issue | 2 business hours / 1 business day |
| P4 — Low | Localised: minor issue, cosmetic, or scheduled minor works | Low | Single workstation slow, non-urgent query | 1 business day / 5 business days |

## Triage rules

1. **Record before you act.** Log the incident with caller, service, symptom, and affected scope before troubleshooting. Unlogged work is unmeasurable work.
2. **Verify the caller.** Confirm identity per the identity verification standard before discussing or changing account details.
3. **Classify with evidence.** Set category, subcategory, and configuration item from the service catalogue. Search the known error database (KEDB) for matching symptoms before deep-diving.
4. **Assign, don't queue.** Route to the assignment group that owns the service, not to the most available person.
5. **Communicate the plan.** Tell the user the priority, the target, and the next update time. For P1, open a major incident and communicate every 30 minutes.
6. **Resolve or escalate — never park.** If the target is at risk, escalate before the breach, not after.

## Escalation paths

- **Functional escalation:** Tier 1 Service Desk → Tier 2 specialist team (Identity, Endpoint, Network, AV, Applications, Security) → Tier 3 vendor or engineering.
- **Hierarchical escalation:** Technician → Team lead → Service Delivery Manager → CIO, triggered for P1 at 60 minutes unresolved or any SLA breach at risk.
- **Major incident:** declare via the major incident process; a Major Incident Manager coordinates comms, resources, and the bridge; incident remains open until service is verified restored.

## Key performance indicators

| KPI | Definition | Target |
| --- | --- | --- |
| MTTA (mean time to acknowledge) | First human/automated response after ticket creation | P1 ≤ 15 min, P2 ≤ 30 min, P3 ≤ 2 business hours |
| MTTR (mean time to resolve) | Creation to resolution, business hours except P1 | Per priority table above |
| First-contact resolution | Incidents resolved at Tier 1 without escalation | ≥ 60% |
| SLA breach rate | Incidents meeting response but missing resolution target, or vice versa | ≤ 5% per month |
| Reopen rate | Incidents reopened within 5 business days | ≤ 3% |

SLA attainment is recorded per incident in `sla-tracker.csv` and reviewed weekly (see `docs/sla-tracking.md`).

## Post-incident requirements

- P1 and P2 incidents that recur within 30 days must raise a problem record (`docs/problem-management.md`).
- P1 incidents require a postmortem within 5 business days using `templates/postmortem.md`.
- Resolution notes must state the fix in operational language another technician could follow — "resolved" alone is not a resolution.
