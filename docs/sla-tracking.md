# SLA Tracking Design

Purpose: turn the SLA targets in `docs/incident-management.md` into measurable data, reviewed on a cadence, with breach causes understood rather than excused. Owner: Service Delivery Manager.

## Data model

Each row of `sla-tracker.csv` is one incident. Fields map to the ITSM incident table (e.g. ServiceNow) so the tracker can be replaced by a report at any time; the CSV is the portable, reviewable artefact.

| Field | Type | Definition |
| --- | --- | --- |
| `incident_number` | text | INC reference, unique |
| `opened_at` | datetime (ISO 8601, AEST/AEDT) | Ticket creation time |
| `priority` | P1–P4 | Per the priority matrix |
| `service` | text | Service catalogue entry name |
| `category` | text | Category/subcategory from triage |
| `assignment_group` | text | Owning team |
| `mtta_minutes` | integer | Minutes from `opened_at` to first response |
| `mttr_minutes` | integer | Minutes from `opened_at` to resolution (elapsed for P1; business hours otherwise) |
| `sla_target_mttr_minutes` | integer | Resolution target for the priority at time of opening |
| `sla_met` | boolean | True when MTTA target **and** MTTR target are both met |
| `breach_reason` | text | Mandatory when `sla_met` is false; categories: staffing, escalation delay, vendor, change-induced, knowledge gap, monitoring gap, requester delay, other |

## How to use it

1. **Capture.** One row per incident, appended by the closing technician (or exported nightly from the ITSM tool using the same field names).
2. **Weekly review.** Service Desk Manager reviews all breaches from the past week: what happened, which reason category, and what prevents recurrence. Breaches without a reason category are returned for completion.
3. **Monthly service report.** Per-service attainment, MTTA/MTTR distribution (median and p90, not just mean), breach reasons ranked, and trends against the previous month.
4. **Quarterly service review.** SLA targets themselves are reviewed against attainment; a target missed every month is either mis-set or the service is under-resourced — both are findings, not background noise.

## Worked queries

```powershell
# Average and p90 MTTR for P2 incidents
$p2 = Import-Csv ./sla-tracker.csv | Where-Object Priority -eq "P2"
($p2.mttr_minutes | Measure-Object -Average).Average
$p2.mttr_minutes | Sort-Object | Select-Object -Index ([int]($p2.Count * 0.9))

# Breach reasons ranked
Import-Csv ./sla-tracker.csv | Where-Object sla_met -eq $false | Group-Object breach_reason | Sort-Object Count -Descending
```

## Governance notes

- Targets are stated per priority (see `docs/incident-management.md`); the tracker measures against the target in force when the incident was opened, not the current target.
- Breach reasons feed problem management: three breaches with the same reason category in a month must raise a problem record.
- The sample rows in `sla-tracker.csv` are illustrative; the fictional Example University data demonstrates the format only.
