# Postmortem: Lecture-Time Wi-Fi Outage (LT-3 and adjacent teaching spaces)

- Incident reference: INC004182 (illustrative)
- Date of incident: Tuesday 18 August 2026
- Severity: P1 — Critical
- Status: Final
- Authors: Service Desk Manager, Network Team lead
- Reviewers: IT Service Delivery Manager, Faculty of Business teaching office

> **Illustrative example.** Example University is fictional. This postmortem is included to demonstrate the format, depth, and follow-through expected of a real postmortem — not to describe a real event.

## Summary

During the 09:00 lecture block, student Wi-Fi failed in lecture theatre LT-3 and three adjacent teaching rooms for 74 minutes. The cause was a personal Wi-Fi router with an active DHCP server, plugged into a wired wall port in LT-3, which answered DHCP requests on the teaching VLAN and exhausted the scope. The device was removed, the scope was cleared, and DHCP snooping was enabled on the affected access switches.

## Impact

- Users affected: approximately 260 students across four teaching spaces, plus 4 lecturers
- Duration: 74 minutes (09:04 first report; 10:18 restoration verified)
- Services affected: Network Connectivity (service catalogue #4)
- Business impact: two lectures moved to pen-and-paper delivery; one lecture capture session lost; 11 follow-up incidents logged by affected students

## Timeline

| Time (AEST/AEDST) | Event |
| --- | --- |
| 09:04 | First student report via service desk chat: "no Wi-Fi in LT-3" |
| 09:07 | Service desk confirms two additional reports in LT-3; P3 raised, Network Team engaged |
| 09:11 | Reports arrive from LT-4 and LT-5; pattern recognised; P2 raised |
| 09:16 | Class actively disrupted in LT-3; P1 declared, major incident bridge opened |
| 09:19 | WLC shows APs healthy and associated; DHCP scope utilisation at 100% |
| 09:24 | Rogue DHCP offer traced to MAC address via switch CAM table to LT-3 wall port |
| 09:31 | On-site technician locates and removes personal router from wall port; port administratively disabled |
| 09:35 | DHCP scope released and leases recovering; first successful student associations observed |
| 09:52 | All four rooms verified by on-site technician and lecturer confirmation |
| 10:18 | Post-incident monitoring confirms no recurrence; major incident closed |

## Detection

Detection was by user report, 4 minutes into impact. The DHCP scope had been trending toward exhaustion for days, but no alert existed on scope utilisation. A DHCP utilisation alert at 80% would have provided roughly 48 hours of warning.

## Root cause

A personal Wi-Fi router with DHCP enabled, connected to a wired wall port in LT-3, acted as a rogue DHCP server on the teaching VLAN and exhausted the legitimate scope, denying addresses to student devices.

## Contributing factors

- No DHCP snooping or port security on access switches in teaching spaces, so the rogue device was able to serve leases.
- No alerting on DHCP scope utilisation.
- The wall port was left enabled outside configured use; no 802.1X or MAC authentication on the teaching VLAN.
- Initial triage focused on the wireless controller (healthy) rather than the DHCP layer, delaying diagnosis by roughly 8 minutes.

## What went well

- The switch from P3 to P2 to P1 was quick and evidence-based once the pattern appeared across rooms.
- The major incident bridge gave the Network Team and on-site technician a single channel; updates to lecturers were sent every 15 minutes.
- The CAM-table trace to a physical port took minutes because switch documentation was current.

## What went badly

- Detection depended entirely on users; the leading indicator (scope utilisation) was visible in the DHCP console but not alerted.
- No runbook existed for "Wi-Fi associated but no address" — a gap now filled by the database/AV-style triage pattern.
- Students in three adjacent rooms had no proactive communication; they learned about the fallback only by asking.

## Action items

| # | Action | Owner | Due date | Status |
| --- | --- | --- | --- | --- |
| 1 | Enable DHCP snooping and ARP inspection on all access switches serving teaching spaces | Network Team lead | 28 August 2026 | Done |
| 2 | Deploy DHCP scope utilisation monitoring with alert at 80% and critical at 90% | Infrastructure Monitoring engineer | 4 September 2026 | Done |
| 3 | Add "associated but no DHCP address" branch to the Wi-Fi triage runbook | Service Desk Manager | 11 September 2026 | Done |
| 4 | Review MAC authentication or 802.1X for teaching-space wall ports; report options to CAB | Network Team lead | 30 September 2026 | Open |
| 5 | Add proactive room-level outage notifications to the status page procedure | IT Service Delivery Manager | 9 October 2026 | Open |

## Lessons learned

"Associated but no address" is a DHCP-layer failure, not a wireless-controller failure — triage must test the address layer before escalating to the WLC vendor. The department now monitors the exhaustion indicator of every DHCP scope, and rogue-device detection is a standing item in the monthly network health check.
