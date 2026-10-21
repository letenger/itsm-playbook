# Change Management Procedure

Applies to: all additions, modifications, or removals affecting university IT services and their supporting infrastructure. Owner: Change Manager. Aligned with ITIL 4 change control.

## Change types

| Type | Authorisation | Lead time | Examples |
| --- | --- | --- | --- |
| Standard | Pre-authorised by CAB; no further approval per occurrence | None (follow the runbook) | Service account password rotation, security patching windows, certificate renewals, adding a known-good printer driver |
| Normal | CAB approval at weekly meeting (or delegated approval for low risk) | 5 business days before implementation | Database schema changes, network switch firmware, M365 tenant configuration changes, new shared mailbox |
| Emergency | Change Manager or delegate, plus retrospective review at next CAB | Immediate, during an incident | Restoring a failed core switch, rolling back a broken deployment, emergency firewall rule to contain an attack |

## Change advisory board (CAB)

- **Cadence:** weekly, Wednesday 10:00–11:00 AEST/AEDT, plus an emergency CAB (ECAB) on demand.
- **Membership:** Change Manager (chair), representatives from Infrastructure, Applications, Security, Service Desk, and a business/teaching representative for teaching-space changes.
- **Quorum:** chair plus at least two technical members; teaching-space changes require the AV or teaching-technology representative.
- **Inputs due:** RFCs submitted by Tuesday 17:00 with risk assessment, implementation plan, test evidence, and rollback plan.
- **Outputs:** approve / approve with conditions / reject / defer, recorded against the RFC number.

## Risk assessment

Every normal and emergency RFC must record:

1. **Impact** — services and user groups affected, worst case if the change fails mid-flight.
2. **Likelihood** — based on prior execution history and test evidence (first execution = higher risk).
3. **Risk level** — Low / Medium / High from the impact × likelihood matrix. High-risk changes require a named implementation lead, a maintenance window, and a tested rollback.
4. **Dependencies** — related RFCs, freezes, vendor scheduling.

## Rollback requirements

- Normal and emergency changes **must** have a documented, tested rollback plan before implementation. "Backup exists" is not a rollback plan.
- The rollback plan must state the trigger (what observation means roll back), the steps, and the maximum time to execute.
- Standard changes must reference the runbook that includes their rollback.
- Changes without a rollback plan may only be approved if failure is provably customer-invisible — this must be argued explicitly, not assumed.

## Change freeze periods

- First two weeks of each semester and the formal examination period: no normal changes affecting teaching spaces, the SIS, or authentication, except emergency changes.
- Emergency changes during a freeze require Change Manager approval and a post-implementation review within 5 business days.

## Emergency change rules

1. Verbal approval from the Change Manager or delegate is sufficient to proceed; document the approver and time in the RFC.
2. The RFC must be completed in the ITSM tool within 24 hours of service restoration.
3. The next CAB reviews all emergency changes and decides: accept, convert to standard (if repeatable), or raise a problem.

## Metrics

- Change success rate (no unplanned outage or rollback): target ≥ 95%.
- Emergency change share of total changes: target ≤ 10%.
- RFC lead time adherence (submitted 5 business days ahead): target ≥ 90%.
