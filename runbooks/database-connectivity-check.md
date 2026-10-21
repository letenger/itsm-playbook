# Runbook: Database Connectivity Check

- **Service:** Line-of-Business Application Support (service catalogue #9)
- **Owner:** Application Support / Database Team
- **Last tested:** 20 September 2026 (illustrative)
- **Execution time:** 15–45 minutes

## Purpose

Diagnose "the application cannot connect to the database" for SQL Server-backed university systems (SIS, LMS, internal web apps). The runbook isolates the fault to one of four layers — network, service, authentication, or application — before escalating.

## Prerequisites

1. Network path to the database subnet (jump host or VPN if the database is not internet-facing — it must not be).
2. `sqlcmd` (part of the SQL Server tooling) or SQL Server Management Studio.
3. Read access to the server's error log, either via `sqlcmd` or the DBA monitoring console.
4. The application's connection details from the CMDB: server FQDN, instance, database name — never accept a connection string from the requester.

## Steps

1. **Record the symptom precisely.** Exact error text, affected users, and whether the application is down or degraded. "Cannot connect" from one user is a different incident from a whole-campus outage.
2. **Test network reachability to the database port:**

   ```powershell
   Test-NetConnection -ComputerName sql-prod-01.example.edu.au -Port 1433
   ```

   A failed TCP test points to network, firewall, or the listener — go to step 5. A successful test points to service or authentication — go to step 3.
3. **Check the SQL Server service and the instance's responsiveness:**

   ```powershell
   Get-Service -Name MSSQLSERVER -ComputerName sql-prod-01.example.edu.au
   sqlcmd -S sql-prod-01.example.edu.au -E -Q "SELECT @@SERVERNAME AS ServerName, @@VERSION AS Version"
   ```

   If the service is stopped, attempt a start and capture the error if it fails — do not restart a clustered instance without the DBA team.
4. **Check authentication and the error log.** Failed logins for the application's service account:

   ```powershell
   sqlcmd -S sql-prod-01.example.edu.au -E -Q "EXEC xp_readerrorlog 0, 1, N'Login failed'"
   ```

   Distinguish: password expired (rotate per the service account runbook), disabled account (Identity Team), or "login is not associated with a trusted connection" (database principal missing — DBA change).
5. **Test from the application host, not the workstation.** Firewall rules are per-subnet; a successful workstation test proves nothing:

   ```powershell
   Enter-PSSession -ComputerName app-prod-01.example.edu.au
   Test-NetConnection -ComputerName sql-prod-01.example.edu.au -Port 1433
   ```

   If the application host cannot reach the database but the workstation can, a recent firewall or network change is the prime suspect — check the change calendar before debugging the application.
6. **Check resource saturation.** High CPU, blocking, or a full tempdb produces timeouts that present as "cannot connect": review the DBA dashboard and the server's performance counters before restarting anything.

## Verification

1. The application's health endpoint returns 200 (or the documented smoke test passes).
2. `sqlcmd` step 3 succeeds from the application host.
3. No new login-failure entries for the application service account in the error log.
4. Update the incident with the isolated layer, the fix, and the evidence.

## Rollback

If a firewall rule, connection string, or credential change was made during diagnosis, revert it to the previous documented value and record the revert in the ticket. Never leave a diagnostic change (e.g. a temporary firewall allow-rule) in place after closure — open a change request if it needs to persist.

## Escalation triggers

- Suspected data corruption, failed failover, or cluster quorum issues → Database Team immediately (P1 if production).
- Suspected unauthorised access (unexpected logins, error log entries from unknown hosts) → Security Team immediately; preserve logs, change nothing.
- Application code or connection string defect confirmed → Application owner, with the isolated evidence attached.
