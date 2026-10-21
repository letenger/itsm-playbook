# Template: Postmortem

Blameless: the postmortem examines systems and processes, not individuals. Required for every P1 incident within 5 business days, and for any P2 the Service Delivery Manager nominates.

```markdown
# Postmortem: <short title>

- Incident reference: INC
- Date of incident: <date>
- Severity: P1 / P2
- Status: Draft / In review / Final
- Authors: <names>
- Reviewers: <service owner, team lead>

## Summary

<Two or three sentences: what happened, who was affected, how it was fixed.>

## Impact

- Users affected: <count or scope>
- Duration: <start of impact to restoration>
- Services affected: <service catalogue entries>
- Business impact: <teaching, research, administrative consequence>

## Timeline

| Time (AEST/AEDT) | Event |
| --- | --- |
| HH:MM | <first symptom / first report> |
| HH:MM | <detection or triage> |
| HH:MM | <key decisions and actions> |
| HH:MM | <restoration verified> |

## Detection

<How did we find out — monitoring, user report, vendor? How long did detection take? What would have detected it sooner?>

## Root cause

<The controllable cause in one or two sentences. 5 Whys chain or Ishikawa reference attached.>

## Contributing factors

<Conditions that made the incident worse or harder to resolve — monitoring gaps, missing runbook step, untested assumption.>

## What went well

<Practices worth keeping.>

## What went badly

<Process, tooling, or communication gaps — stated without blame.>

## Action items

| # | Action | Owner | Due date | Status |
| --- | --- | --- | --- | --- |
| 1 | <action> | <named person> | <date> | Open / Done |
| 2 | | | | |

## Lessons learned

<What the department now knows that it did not know before.>
```

Rules: every action item has a named owner and a due date; "monitor the situation" is not an action item; action items are reviewed at the monthly problem review board until closed.
