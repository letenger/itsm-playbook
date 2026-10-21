# Service Catalogue — Example University IT Services

Owner: IT Service Delivery Manager. Reviewed quarterly by each service owner. Changes follow the change process in `change-management.md`.

| # | Service | Description | SLA target (response / resolution) | Responsible team | Escalation path |
| --- | --- | --- | --- | --- | --- |
| 1 | Account and Password Support | Self-service password reset (SSPR) assistance, MFA authenticator reset, account unlock, sign-in troubleshooting for M365 and university systems | P3: 2 business hours / 1 business day | Service Desk (Tier 1) | Identity team (Tier 2) → M365 tenant administrators (Tier 3) |
| 2 | Endpoint Support | Staff laptop and desktop provisioning, imaging, hardware faults, peripheral setup, warranty repairs | P3: 4 business hours / 3 business days | Endpoint Team | Endpoint Team lead → hardware vendor |
| 3 | Classroom AV and Lecture Theatre Support | Projection, lecture capture, room audio, control panels (Crestron/AMX), lectern PCs, room readiness checks | P2 during teaching: 30 minutes / 4 hours; P3 outside teaching | AV Team | AV on-call technician → AV vendor |
| 4 | Network Connectivity | Wired and Wi-Fi access, VPN, residence network, guest access, network fault diagnosis | P2: 30 minutes / 8 business hours; P1 for campus-wide outage: 15 minutes / 4 hours | Network Team | Network Team lead → network vendor / carrier |
| 5 | Printing and Scanning | Staff and student print queues, follow-me printing, MFD faults, scan-to-email, print accounting | P3: 4 business hours / 2 business days | Service Desk → Print Services | Print Services lead → MFD vendor |
| 6 | Email and Collaboration | M365 mail, Teams, SharePoint, OneDrive, shared mailbox and distribution list administration | P3: 2 business hours / 1 business day | Service Desk (Tier 1) | Collaboration Team → Microsoft support |
| 7 | Software Licensing and Installation | Licensed software requests, media and activation keys, installation support, licence compliance reporting | P4: 1 business day / 5 business days | Software Licensing | Licensing administrator → software reseller |
| 8 | Staff Onboarding and Offboarding | Account creation, group and licence assignment, equipment issue, access removal on separation | Requested 5 business days before start / same day for offboarding | Service Desk | HR liaison → Identity team |
| 9 | Line-of-Business Application Support | Student information system (SIS), learning management system (LMS), finance and HR systems, internal web apps | P2: 30 minutes / 8 business hours | Application Support | Application owner → software vendor |
| 10 | Security Incident Triage | Phishing reports, malware alerts, account compromise indicators, lost device reports | P1 suspected compromise: 15 minutes / 4 hours | Security Team | Security Team lead → CISO delegate |

## Using the catalogue

- **Staff** request services through the self-service portal, which renders these entries as catalogue items; the portal shows each service's target so expectations are set before a ticket exists.
- **Service desk** uses this catalogue as the authoritative classification source during triage: the service entry determines the assignment group, the SLA target, and the escalation path.
- **Service owners** review their entry quarterly and after any major incident; proposed changes follow `change-management.md` so target changes are approved, not edited silently.

## Notes

1. **Business hours** are 08:00–18:00 AEST/AEDT, Monday to Friday, excluding public holidays. P1 targets apply 24×7.
2. **Priority definitions** are in `docs/incident-management.md`. SLA targets above are expressed per priority, not per service.
3. **Service requests** (standard changes such as software installs, access grants) follow the request fulfilment path: service catalogue item → approval (where required) → fulfilment → closure. They are not incidents and must not be logged as incidents.
4. **Service owners** must review their entry quarterly and after any major incident affecting their service. Stale SLA targets are treated as a known error, not a documentation detail.
5. The catalogue is mirrored into the ITSM tool (e.g. ServiceNow Service Catalog) so that staff request services directly; this document is the source of truth for targets and ownership.
