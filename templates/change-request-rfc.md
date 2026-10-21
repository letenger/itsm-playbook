# Template: Change Request (RFC)

Copy into the change record in the ITSM tool. All fields are mandatory for normal changes; emergency changes may complete sections 4–6 within 24 hours of service restoration.

```markdown
## Identification

- RFC number: CHG
- Requested by: <name, team>
- Change type*: Standard / Normal / Emergency
- Title*: <one line, verb first>
- Related incident / problem: INC / PRB

## Justification

- Reason / business driver*: <what breaks or what improves without this change>
- Consequences of not changing*: <risk of inaction>

## Scope

- Affected services*: <service catalogue entries>
- Affected CIs*: <CMDB references>
- Affected user groups*: <who notices if it fails>
- Implementation window*: <date, start–end, timezone>

## Assessment

- Impact*: <worst case if the change fails mid-flight>
- Likelihood*: <based on prior executions and test evidence>
- Risk level*: Low / Medium / High
- Dependencies*: <other RFCs, vendor actions, freeze periods>

## Plan

- Implementation steps*: <numbered, with verification after each step>
- Test plan / evidence*: <what was tested, where, by whom, result>
- Rollback plan*: <trigger observation, steps, maximum time to execute>
- Communication plan*: <who is told what, before and after>

## Authorisation

- CAB date: <date>
- CAB decision*: Approved / Approved with conditions / Rejected / Deferred
- Conditions / approver notes: <text>
- Emergency approval (if applicable): <approver, time>

## Post-implementation

- Implemented by / at: <name, timestamp>
- Outcome*: Successful / Rolled back / Partially successful
- Post-implementation review*: <within 5 business days; findings>
```

Review gate: no normal change enters the CAB without a tested rollback plan. "A backup exists" is not a rollback plan.
