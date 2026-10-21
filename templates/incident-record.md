# Template: Incident Record

Copy into the incident record in the ITSM tool. Fields marked * are mandatory before assignment. Field names map to ServiceNow Incident module equivalents in brackets.

```markdown
## Identification

- Incident number*: INC
- Opened*: <date time, AEST/AEDST>
- Opened by*: <technician or auto-channel>
- Reported by*: <name, verified identity per standard>
- Contact*: <phone / email>
- Major incident*: Yes / No

## Classification

- Service*: <service catalogue entry>
- Category / subcategory*: <e.g. Network / Wi-Fi>
- Configuration item: <CMDB CI, e.g. wlc-core-01.example.edu.au>
- Assignment group*: <owning team per service catalogue>

## Prioritisation

- Impact*: Extensive / Significant / Limited / Localised
- Urgency*: Immediate / High / Medium / Low
- Priority*: P1 / P2 / P3 / P4 (see priority matrix)
- SLA response target*: <auto from priority>
- SLA resolution target*: <auto from priority>

## Detail

- Symptom*: <observable, user's words plus evidence>
- Scope*: <users, rooms, systems affected>
- Business impact*: <teaching, research, admin impact>
- KEDB searched*: Yes / No — <KE reference if matched>
- Actions taken*: <time-stamped, chronological>
- Communications sent: <audience, channel, time>

## Resolution

- Resolution code*: <e.g. Solved / Workaround / No fault found>
- Resolution notes*: <operational language another technician could follow>
- Root cause (if known): <one or two sentences; PRB reference if problem raised>
- First response at*: <timestamp>
- Resolved at*: <timestamp>
- Reopened count: <n>
- Related problem: PRB
```

Completion rules: every field marked * must be populated before the incident is assigned; resolution notes are mandatory before closure; "resolved" alone is not a resolution note.
