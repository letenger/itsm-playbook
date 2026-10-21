# ITSM Playbook — Example University IT Services

A working IT service management (ITSM) playbook for a mid-sized university IT department, published as a portfolio artefact for IT support, ITSM, and service desk roles in Canberra government and university environments.

**Example University is fictional.** Every name, hostname, ticket number, and incident in this repository is illustrative and written for demonstration purposes only. Nothing here describes a real institution.

## What this is

This repository is the service delivery half of an engineering portfolio. It contains the documents a real IT department runs on day to day: a service catalogue with SLA targets, incident and change procedures, runbooks an on-call technician can execute at 2 a.m., templates that make ticket and change records consistent, a completed postmortem, and an SLA tracker with a defined data model.

It is written in ITIL 4 vocabulary — incident, problem, change, known error database (KEDB), change advisory board (CAB), MTTA/MTTR, SLA/SLO — because that is the vocabulary of the employers I am targeting, and because shared vocabulary is the difference between a service desk and a help desk.

## Who this is for

- **Hiring managers and panels** in Canberra government and university IT teams evaluating whether a candidate understands service delivery, not only code.
- **Practitioners** who want a concrete starting point for their own team's documentation.

## How to read it

Fifteen-minute path for reviewers:

1. `docs/incident-management.md` — how priorities, triage, and escalation actually work.
2. `runbooks/` — executable procedures with real commands, verification, and rollback.
3. `postmortems/` — one complete, honest postmortem with dated action items.
4. `docs/sla-tracking.md` — how service performance is measured and reviewed.

Full path for practitioners: service catalogue → incident → change → problem → runbooks → templates → postmortems → onboarding → SLA tracking.

## Engineering mindset applied to service delivery

Most candidates show code; fewer show operations; almost none show service management. I treat service delivery the way I treat a production system:

- **Versioned documentation.** Runbooks live in Git, change through review, and have a commit history — the same discipline as source code.
- **Measurable targets.** Every priority has an MTTA/MTTR target, and the SLA tracker turns those targets into data that gets reviewed, not filed.
- **Executable procedures.** A runbook that cannot be followed at 2 a.m. by someone who did not write it is not finished. Every runbook states prerequisites, commands, verification, rollback, and escalation triggers.
- **Feedback loops.** Every major incident produces a postmortem with named owners and due dates; recurring issues graduate to problem management with a known error record.

## ITIL 4 alignment

| ITIL 4 practice | Document |
| --- | --- |
| Service catalogue management | `docs/service-catalogue.md` |
| Incident management | `docs/incident-management.md` |
| Change control | `docs/change-management.md` |
| Problem management | `docs/problem-management.md` |
| Knowledge management | `docs/problem-management.md` (KEDB), `runbooks/` |
| Service level management | `docs/sla-tracking.md`, `docs/sla-tracker.csv` |

## ServiceNow concept mapping

| Playbook concept | ServiceNow module |
| --- | --- |
| Service catalogue entries | Service Catalog (items, record producers) |
| Incident priority and triage | Incident (priority, impact, urgency, assignment groups) |
| Change types and CAB | Change (standard, normal, emergency; CAB workbench) |
| Known error records | Knowledge (KB articles), Problem |
| Runbooks | Flow Designer runbooks / Knowledge articles |
| SLA targets | SLA Definitions attached to task tables |
| Metrics | Performance Analytics, Reports and Dashboards |
| Affected assets | Configuration Items (CMDB) |

## Repository layout

```text
itsm-playbook/
├── README.md
├── docs/
│   ├── service-catalogue.md      # 10 services with SLA targets and escalation paths
│   ├── incident-management.md    # priority matrix, triage, escalation, KPIs
│   ├── change-management.md      # change types, CAB, risk, rollback
│   ├── problem-management.md     # problem vs incident, KEDB, RCA
│   ├── sla-tracking.md           # SLA data model and review cadence
│   └── sla-tracker.csv           # sample incident-level SLA data
├── runbooks/
│   ├── service-account-password-reset.md
│   ├── classroom-av-triage.md
│   └── database-connectivity-check.md
├── templates/
│   ├── incident-record.md
│   ├── change-request-rfc.md
│   └── postmortem.md
├── postmortems/
│   └── 2026-illustrative-lecture-wifi-outage.md
└── onboarding/
    └── it-support-onboarding.md
```

## Conventions

- Australian English spelling throughout (organisation, authorisation, prioritise).
- Priority labels P1–P4, defined in `docs/incident-management.md`.
- "Must" denotes a mandatory control; "should" denotes a strong default that may be waived with a recorded reason.
- All PowerShell examples target Windows PowerShell 5.1 or PowerShell 7+ with the Microsoft Graph PowerShell SDK.
