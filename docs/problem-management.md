# Problem Management Procedure

Applies to: diagnosis and elimination of the root causes of incidents. Owner: Problem Manager. Aligned with ITIL 4 problem management.

## Incident vs problem

| Dimension | Incident | Problem |
| --- | --- | --- |
| Goal | Restore service as fast as possible | Identify and remove the root cause |
| Time pressure | Minutes to hours | Days to weeks |
| Typical action | Workaround, restart, failover | Analysis, trend review, permanent fix |
| Record | Incident (INC) | Problem (PRB) |
| Success measure | MTTR against SLA | Recurrence eliminated |

A problem may be raised from a single significant incident (any P1) or from a pattern: three or more similar incidents on the same service within 30 days must trigger a problem review.

## Problem lifecycle

1. **Identify** — detect via incident trends, major incident postmortems, monitoring alerts, or staff reports.
2. **Investigate** — reproduce where safe, gather logs and timelines, quantify impact and cost of recurrence.
3. **Root cause analysis** — required for all P1-derived problems. Acceptable methods: 5 Whys (minimum), Ishikawa (fishbone) for multi-factor causes. Stop at a cause that can be controlled, not at "human error".
4. **Workaround** — document an interim workaround and register it as a known error so the service desk can apply it immediately.
5. **Resolve** — deliver the permanent fix through the change process; verify the fix against the original failure evidence.
6. **Close** — confirm recurrence is absent for an agreed observation period, then close and update the KEDB.

## Known error database (KEDB)

The KEDB is the shared memory of the department. It lives in the ITSM knowledge base and is mirrored for offline access by the on-call technician.

Required fields for each known error record:

| Field | Content |
| --- | --- |
| Known error ID | `KE-<number>` |
| Symptom | What the user or monitor reports, in observable terms |
| Affected service / CI | Service catalogue entry and configuration item |
| Root cause | The controllable cause, one or two sentences |
| Workaround | Steps the service desk can execute immediately (link a runbook where one exists) |
| Permanent fix status | Not started / In change pipeline / Implemented (RFC number) |
| Linked problem / incidents | PRB and INC references |

Search order during triage: KEDB symptom search before deep diagnosis. A KEDB hit with a workaround typically converts a P2 into a P3.

## Root cause analysis requirements

- Written RCA is mandatory for every P1-derived problem and any problem whose recurrence cost exceeds 8 staff-hours.
- RCA must distinguish root cause from contributing factors, and must not stop at "user error" without asking what the system allowed or failed to prevent.
- Action items from RCAs follow the postmortem convention: named owner, due date, tracked to closure at the monthly problem review.

## Review cadence and metrics

- **Monthly problem review board:** Problem Manager chairs; all open problems and KEDB additions are reviewed; recurring incidents per service are trended.
- **Metrics:** problems identified vs closed per quarter; percentage of incidents resolved via a KEDB workaround (target ≥ 25% of P2/P3); reduction in repeat incidents for services with closed problems (target −50% within 90 days of closure).
