# Runbook: Classroom AV Failure Triage

- **Service:** Classroom AV and Lecture Theatre Support (service catalogue #3)
- **Owner:** AV Team
- **Last tested:** 2 October 2026 (illustrative)
- **Execution time:** 10–30 minutes depending on fault layer

## Purpose

Restore teaching capability in a lecture theatre or classroom when projection, audio, or the control system fails. During teaching hours this is a P2 with a 30-minute response target; treat it as P1 if a class is actively disrupted and no alternative room is immediately available.

## Prerequisites

1. Physical access to the room, or confirmed on-site technician (remote triage is limited to steps 1–3).
2. Room asset details from the CMDB: control processor hostname (e.g. `lt3-ctrl-01.example.edu.au`), display model, lectern PC name.
3. AV on-call phone number and the AV vendor support contract reference.
4. A known-good test laptop with HDMI and USB-C adapters.

## Steps

1. **Confirm scope.** Check the timetable for the room. A failure 10 minutes before a lecture is P2; a failure with 200 students seated is P1 — declare a major incident and notify the AV on-call technician immediately.
2. **Check the obvious.** Display power and input source; lectern PC powered and logged in; control panel awake and showing the room page; cables seated at the lectern.
3. **Test the signal path.** Connect the test laptop to the lectern HDMI. If the display shows the laptop, the fault is in the lectern PC or its switching; if not, the fault is downstream (display, matrix, or cabling).
4. **Check the control system.** From the network, confirm the control processor responds:

   ```powershell
   Resolve-DnsName lt3-ctrl-01.example.edu.au
   Test-NetConnection -ComputerName lt3-ctrl-01.example.edu.au -Port 443
   ```

   If the processor is unreachable, the control panel may be operating standalone — use the panel's local display on/off and input buttons as the immediate workaround, then escalate for processor replacement.
5. **Reboot in the documented order.** Power off the display, wait 30 seconds, power on; if unresolved, reboot the control processor (labelled reset button or managed PDU outlet); if still unresolved, reboot the lectern PC. Rebooting out of order can drop the control processor's room configuration.
6. **Check consumables and logs.** Display lamp or laser hours near end of life explain gradual dimming; the vendor portal shows the last fault codes for the display.
7. **Fallback for teaching continuity.** If resolution will exceed 15 minutes, arrange an alternative room via the timetabling office and post signage on the affected room.

## Verification

1. Lecturer laptop (not the test laptop) projects at native resolution with audio at usable level.
2. Control panel operates display on/off, input switching, and volume.
3. Lecture capture (if fitted) records and is retrievable.
4. Room marked restored in the ticket; if a fallback room was arranged, confirm the return to the original room for the next scheduled class.

## Rollback

This runbook is diagnostic; no configuration change is made except a control processor reboot. If the processor was factory-reset or replaced, restore the room configuration from the AV configuration backup (stored in the AV team repository) and re-verify every input and the capture system.

## Escalation triggers

- Display, projector, or matrix hardware fault confirmed → AV vendor ticket within warranty SLA, with room and fault code.
- Control processor replacement needed → change record (normal) with configuration restore; teaching continuity plan required before the swap.
- Two or more rooms fail in the same week with similar symptoms → raise a problem record (possible firmware or configuration issue).
