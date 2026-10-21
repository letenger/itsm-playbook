# Runbook: Service Account Password Reset

- **Service:** Account and Password Support (service catalogue #1)
- **Owner:** Identity Team
- **Last tested:** 14 September 2026 (illustrative)
- **Execution time:** 10–15 minutes

## Purpose

Reset the password of a non-interactive service account in Microsoft Entra ID when the credential has expired, been compromised, or must be rotated per the standard change schedule. Service accounts must never be reset by editing the account interactively or by reusing a human password.

## Prerequisites

1. A Privileged Role Administrator or Global Administrator account — service account resets must not be performed from a Tier 1 account.
2. Microsoft Graph PowerShell SDK installed: `Install-Module Microsoft.Graph -Scope CurrentUser`.
3. An approved ticket or RFC number (rotation schedule, or incident/security reference).
4. The list of dependent systems from the service owner (scheduled tasks, app registrations, printers, backup jobs). If unknown, stop and request it — a blind reset causes a second incident.
5. Access to the credential store (Azure Key Vault or the privileged access management system) to publish the new secret.

## Steps

1. Record the start time and ticket number in the ticket.
2. Connect to the tenant with least-privilege scopes:

   ```powershell
   Connect-MgGraph -Scopes "User.ReadWrite.All","Directory.Access.As.All" -TenantId "example.edu.au"
   ```

3. Confirm the target account and its current sign-in status before changing anything:

   ```powershell
   Get-MgUser -UserId "svc-print@example.edu.au" -Property DisplayName,AccountEnabled,PasswordPolicies | Format-List
   ```

4. Generate a new 36-character password meeting complexity requirements and apply it. The GUID guarantees length; the suffix guarantees character classes:

   ```powershell
   $securePassword = ConvertTo-SecureString ((New-Guid).Guid + "Aa1!") -AsPlainText -Force
   Update-MgUser -UserId "svc-print@example.edu.au" -PasswordProfile @{ Password = $securePassword; ForceChangePasswordNextSignIn = $false }
   ```

   For a break-glass or emergency rotation where the account is believed compromised, also revoke refresh tokens: `Revoke-MgUserSignInSession -UserId "svc-print@example.edu.au"`.

5. Publish the new credential to the credential store and update the service owner's configuration (scheduled task, app setting, or printer config) using their documented procedure.
6. Record the change in the CMDB entry for the service account: date, RFC/ticket, operator, dependent systems updated.

## Verification

1. The dependent service authenticates successfully — run the service owner's smoke test, or for a print service account confirm the queue accepts a test job.
2. Sign-in logs (Entra ID → Sign-in logs, filter on the account) show a successful service principal sign-in after the reset.
3. No new "account locked out" alerts for the account within 30 minutes.

## Rollback

There is no rollback of a password reset. If verification fails: re-run steps 4–5 with a new credential, check whether a second system is still using the old credential (the usual cause), and raise a problem record if the dependency list was incomplete.

## Escalation triggers

- Evidence the account was used maliciously → raise a security incident (P1) and hand to the Security Team; do not continue.
- The dependency list is unknown or the account is used by more than three systems → escalate to the application owner before resetting.
- The account holds a privileged role → require a second administrator to approve and witness the reset.
