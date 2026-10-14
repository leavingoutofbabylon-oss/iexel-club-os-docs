# B4D-04A Supervised Backup Operator Runbook (Revision 2)
**Document Reference:** `B4D-04A-DOC-02-R2`  
**Classification:** Restricted Operator Procedure  
**System:** IEXEL Club OS (Grassroots Football Club Management)  
**Authoritative Baselining:** Commit `452b30312dcc16ad3b1c6c7d0d74503b27c5c9bc`  
**Synthetics Baseline:** 117 Passing Synthetic Unit & Security Tests  
**Operational Status:** Read-Only Operator Runbook — Live Operations Strictly Prohibited  

---

## 1. Executive Summary & Operational Boundaries

This runbook specifies the operator protocol for the first supervised encrypted backup of the IEXEL Club OS development environment into the `IEXEL_RC_VAULT` container.

### Mandatory Operational Boundaries:
1. **Execution Mode is Blocked in Code:** In baseline `452b30312dcc16ad3b1c6c7d0d74503b27c5c9bc`, `Invoke-ClubOsBackupPackaging.ps1` contains an unconditional blocker preventing Execution mode (`-Mode Execution`). No command-line switch, parameter, environment variable, or wrapper script can bypass this blocker.
2. **Zero Out-of-Band Bypass:** Operators **must not** attempt to bypass, unhook, or alter the backup script outside of an authorized, peer-reviewed engineering batch approved by the Product Owner.
3. **All Live Commands are Strictly Prohibited:** Every command in this runbook that modifies state, mounts the BitLocker vault, accesses credentials, or writes data is marked **PROHIBITED** until the corresponding Product Owner Approval Gate is formally granted.
4. **Three Independent Approval Gates:**
   - **Gate B:** Authorization to place the environment into maintenance mode and suspend workers.
   - **Gate C:** Authorization to lift the execution blocker in a dedicated batch and execute the supervised backup.
   - **Gate D:** Authorization to replicate the encrypted backup to an approved off-device destination.

---

## 2. Source Quiescence: Principles, Limits, & Evidence Standards

A reliable backup requires an internally coherent, write-free state across both the relational database and the recoverable filesystem. Achieving and proving this requires clear distinction between different consistency models and an understanding of monitoring limitations.

### 2.1 Transactional SQL Snapshots vs. Combined Consistent Backups
- **The Transactional SQL Snapshot (`mysqldump --single-transaction`):** Within InnoDB, `--single-transaction` starts a repeatable-read transaction, guaranteeing that the dumped SQL tables represent a consistent snapshot *at the moment the dump transaction began*.
- **The Combined Database/Filesystem Coherence Problem:** A Club OS backup includes both the MySQL database and the WordPress filesystem (`files.zip` containing uploads, plugins, logs, and attachments). A database transactional snapshot does **not** synchronize with filesystem I/O. If a user uploads an emergency medical consent form or updates a team roster image while `database.sql` is halfway through export, the resulting `database.sql` and `files.zip` will be out of sync.
- **The Quiescence Imperative:** True coherence requires complete cessation of writes across both tiers for the entire duration of the backup packaging process.

### 2.2 Limitations of Global MySQL Counters (Correction B)
The runbook strictly prohibits relying on global MySQL counters (e.g., `Handler_write`, `Innodb_rows_inserted`, `Com_insert`) as independent proof that the target database is write-free:
1. **Server-Wide Scope:** Global status variables aggregate activity across the entire MySQL server instance. In LocalWP or shared environments, internal system schemas (`mysql`, `information_schema`, `performance_schema`, `sys`), sibling test schemas, or LocalWP telemetry processes run concurrently on the same MySQL daemon.
2. **Background Engine Activity:** Internal MySQL background threads (e.g., InnoDB master thread purge, page flushing, dirty buffer writing, undo log truncation) increment global write counters even when the target database has zero client queries.
3. **False Positives & Ambiguity:** A change in a global counter does not prove that schema `local` was modified, and an unchanged global counter does not prove that no uncommitted memory transactions were in flight.
4. **Distinction Required:** Database-specific evidence must be isolated from general server activity.

### 2.3 Individual Checks Cannot Prove Quiescence
- **`.maintenance` Alone is Insufficient:** Only intercepts standard HTTP web traffic entering via `index.php`. Does not intercept WP-CLI commands, system cron jobs, LocalWP background workers, direct database sockets, or external API endpoints.
- **Process-List Polling Alone is Insufficient:** Sampling `information_schema.processlist` checks only a single microsecond slice of time. Fast write queries or queued asynchronous jobs can easily execute between polling intervals.
- **Filesystem Timestamps Alone are Insufficient:** Only reflect past writes that have been flushed to disk; cannot detect in-memory buffers or open file streams.

### 2.4 Multi-Layered Quiescence & Continuous Monitoring Standard
To achieve reliable quiescence:
1. **Operator-Enforced Cessation of All Known Write Sources:** Inbound web traffic, scheduled crons, Action Scheduler workers, and host background processes must be explicitly suspended.
2. **Pre-Monitoring Source Identity Verification:** Confirm database host (`127.0.0.1`), port (`10012`), database name (`local`), siteurl (`http://iexel-club-os-dev.local`), and table count before establishing any monitoring baseline.
3. **Continuous Monitoring Strategy:**
   - **Database Tier:** Monitor database-specific indicators scoped strictly to `table_schema = 'local'` (e.g., tracking `information_schema.tables.UPDATE_TIME`, inspecting `information_schema.innodb_trx` for active transactions on schema `local`, and monitoring schema table row checksums).
   - **Filesystem Tier:** Continuously monitor `wp-content/uploads/` and plugin directories for filesystem creation, modification, or deletion events.
4. **Fail-Closed Abort Policy:** If any monitoring gap occurs (e.g., connection timeout, query parsing failure), or if any unexpected write event is detected on schema `local` or the filesystem during packaging, the pipeline must **immediately abort, fail closed, and trigger rollback**.
5. **Outstanding Prerequisite:** Where an automated, continuous, source-specific monitoring harness is not yet implemented in tooling, this capability is marked as an **unresolved prerequisite for Gate B/C**; operators must not assume polling alone provides proof.

---

## 3. Maintenance Ownership, Tracking, & Restoration (Correction A)

To prevent accidental disruption of pre-existing administrative maintenance, ensure clean restoration of services, and establish ownership over maintenance artifacts, the operator must execute the following protocol:

### 3.1 Pre-Existing State Recording (Pre-Gate B)
Before touching any service or file, the operator performs a read-only audit:
1. **Inspect `.maintenance`:** Check whether `.maintenance` already exists in the WordPress root (`c:\Users\leavi\Local Sites\iexel-club-os-dev\app\public`). Record its existence (`$true`/`$false`), size, creation timestamp, and SHA-256 hash in the preflight log.
2. **Refuse to Overwrite (Fail-Closed Rule):** If `.maintenance` already exists, the operator **MUST NOT OVERWRITE** or adopt it. The procedure must halt immediately. Overwriting would destroy pre-existing administrative context and risk premature removal of an unassociated administrative lock.
3. **Record Original State of Background Services:**
   - **WP-Cron:** Record if `DISABLE_WP_CRON` is set in `wp-config.php` and whether system cron tasks are active.
   - **Action Scheduler:** Record current queue status (count of `pending`, `in-progress`, `complete`, and `failed` actions).
   - **LocalWP Background Services:** Record running process list and synchronization status.
   - Only services actively running before the maintenance window are recorded as eligible for restoration.

### 3.2 Authorised Maintenance Creation & Ownership Inscription (Gate B)
When Gate B is formally authorized:
1. Generate a cryptographically secure, unique run token:
   `$RunToken = [Guid]::NewGuid().ToString('N')`
2. Create `.maintenance` containing embedded provenance markers:
   ```php
   <?php
   // IEXEL_CLUB_OS_MAINTENANCE_MARKER
   // RunToken: [UNIQUE_RUN_TOKEN]
   // CreatedAtUtc: [ISO_8601_TIMESTAMP]
   // OperatorId: [OPERATOR_IDENTIFIER]
   $upgrading = time();
   ?>
   ```
3. Record the generated token, file creation timestamp, byte size, and SHA-256 hash in the run tracker as positive proof of ownership.

### 3.3 Ownership Verification Prior to Removal
Before removing `.maintenance` during completion or rollback:
1. Re-read `.maintenance` from disk.
2. Verify that the file content contains the exact `RunToken` generated in Step 3.2.
3. Verify that the file SHA-256 matches the recorded creation hash.
4. **Anomaly Detection & Stop-Condition:** If `.maintenance` is missing, or if its token/hash/timestamp has been altered (indicating external administrative intervention or unexpected modification during the window), **DO NOT REMOVE THE FILE**. Halt execution immediately, flag `MAINTENANCE OWNERSHIP ANOMALY`, and escalate for manual investigation.
5. If and only if ownership is positively verified, remove `.maintenance`.

### 3.4 Selective Service Restoration & Verification Plan
1. **Selective Restoration:** Restore **only** those services that were recorded as running prior to maintenance and were explicitly suspended by this operation. Services that were already stopped before the maintenance window must remain stopped.
2. **Restoration Execution:**
   - Re-enable Action Scheduler workers.
   - Re-enable WP-Cron / system cron tasks.
   - Resume LocalWP background services.
3. **Post-Restoration Verification:**
   - Verify WordPress HTTP status returns `200 OK` (or pre-existing status).
   - Confirm Action Scheduler resumes queue processing without error.
   - Confirm MySQL exhibits normal, expected query processing.
4. **Safe Escalation on Restoration Failure:**
   - If service restoration fails (e.g., workers fail to start or background queues stall), leave `.maintenance` in place if ownership is verified, log all diagnostic errors to `maintenance_escalation.log`, and immediately escalate to the Lead Systems Administrator and Product Owner.

---

## 4. Supervised Live Backup Execution (PROHIBITED PENDING GATE C)

> [!CAUTION]
> **OPERATIONAL GATE C REQUIRED:** Live execution is unconditionally blocked in the code baseline (`452b30312dcc16ad3b1c6c7d0d74503b27c5c9bc`).  
> Live execution requires a separate, dedicated, peer-reviewed engineering batch (B4D-04C) that introduces the authorized execution harness under dual-operator control. Do not attempt out-of-band execution.

### Step 1: Pre-Attach and Unlock BitLocker Vault Container
1. Operator attaches the approved virtual disk:
   ```powershell
   # PROHIBITED PENDING FORMAL GATE C APPROVAL
   $VhdxPath = "C:\Users\leavi\.codex\private-backups\iexel-rc-VYqEpdwXa\rc-vault.vhdx"
   Mount-DiskImage -ImagePath $VhdxPath -StorageType VHDX -AccessMode ReadWrite
   ```
2. Interactively unlock the BitLocker volume using authorized operator credentials.
3. Confirm volume label is `IEXEL_RC_VAULT`.
4. Confirm Key Protector GUID matches `43B93322-B1D6-4554-A614-3A58866B5DB0`.
5. Confirm minimum free disk space exceeds 2 GiB (2,147,483,648 bytes).
6. Confirm destination root contains zero pre-existing backup package files (`database.sql`, `files.zip`, `IEXEL_BACKUP_MANIFEST.json`, `PROVENANCE.json`, `CHECKSUMS.sha256`).

### Step 2: Supervised Pipeline Execution
1. The authorized execution harness runs `Invoke-ClubOsBackupPackaging.ps1` with verified parameters:
   - `-Mode Execution`
   - `-SourceRoot "c:\Users\leavi\Local Sites\iexel-club-os-dev\app\public"`
   - `-TargetVaultRoot "<Assigned_Vault_Drive_Letter>:\"`
   - `-ApprovedSourceSiteUrl "http://iexel-club-os-dev.local"`
   - `-DatabasePort 10012`
   - `-DatabaseName "local"`
   - `-QuiescentEnvironmentConfirmed`
   - `-MaintenanceModeConfirmed`
2. **Artifact Ownership Tracking:** `New-BackupRunTracker` registers every transient `.tmp` and finalized artifact.
3. **Secure Credential Handling:** Temporary database defaults file (`my.cnf`) is generated in an exclusive, ACL-restricted staging directory, referenced via `--defaults-extra-file`, and wiped with 512 zero-bytes immediately upon export completion.
4. **Continuous Quiescence Enforcement:** Continuous monitoring of schema `local` and the uploads directory runs in parallel. Any detected write triggers an immediate abort.

### Step 3: Verify Output Package Contract
Confirm the pipeline has produced the exact five standard artifacts in the root of the vault volume:
1. `database.sql` (Verified with `-- Dump completed on YYYY-MM-DD` tail marker)
2. `files.zip` (Verified entry count matches manifest; zero ZipSlip traversal entries)
3. `PROVENANCE.json` (Captures Git HEAD `452b30312dcc16ad3b1c6c7d0d74503b27c5c9bc`, clean tree, WP/PHP/MySQL versions)
4. `IEXEL_BACKUP_MANIFEST.json` (Cryptographic manifest containing SHA-256 hashes of all artifacts and database table count at property path `Database.TableCount`)
5. `CHECKSUMS.sha256` (Standard Unix format hash list for storage re-read verification)

### Step 4: Dismount & Lock Vault Container
1. Immediately dismount and lock the BitLocker volume:
   ```powershell
   # PROHIBITED PENDING FORMAL GATE C APPROVAL
   Lock-BitLocker -MountPoint "<Assigned_Vault_Drive_Letter>:" -ForceDismount
   Dismount-DiskImage -ImagePath $VhdxPath
   ```
2. Confirm virtual disk status is detached.

---

## 5. Operator-Controlled Rollback & Ownership-Safe Cleanup

If an error or monitoring anomaly occurs during execution, execute the following rollback:

### Step 1: Run-Owned Artifact Rollback
- The pipeline's rollback routine (`Invoke-RunRollbackCleanup`) deletes **only** registered, run-owned artifacts.
- **Strict Rule:** Pre-existing files in the target directory that were present prior to the run are **never** deleted.
- If cleanup fails on any file, report `ROLLBACK CRITICAL FAILURE` and halt for manual operator inspection.

### Step 2: Ownership-Verified Maintenance Teardown
- Follow Section 3.3: verify `RunToken` and creation hash before removing `.maintenance`.
- If the token does not match or was altered, stop and escalate.
- Follow Section 3.4: selectively restore only those services that were running prior to maintenance.

### Step 3: Credential Eradication Audit
- Verify that any transient credential directory under `$env:USERPROFILE\.codex\` has been zero-filled and removed.

---

## 6. Off-Device Replication & Custody Transfer (PROHIBITED PENDING GATE D)

> [!WARNING]
> **OPERATIONAL GATE D REQUIRED:** Replicating the encrypted backup container to secondary media requires explicit Product Owner approval under a separate, dedicated execution batch (B4D-04D).

### Step 1: Destination Approval & Pre-Copy Validation
1. **Explicit Destination Approval:** The destination path (e.g., dedicated hardware-encrypted external volume or secure network repository) must be formally approved by the Product Owner. No hardcoded drive letters (e.g., `E:`) are assumed.
2. **Capacity Verification:** Operator confirms the destination device has sufficient free capacity to hold the full VHDX container (~452 MB minimum, plus 20% headroom).
3. **Collision Prevention:** Operator inspects destination path. **Overwriting existing files is strictly prohibited.** If a file with the target name already exists, the copy must fail closed.

### Step 2: Controlled Transfer
1. Copy the closed `rc-vault.vhdx` file to the approved destination:
   ```powershell
   # PROHIBITED PENDING FORMAL GATE D APPROVAL
   $ApprovedDestPath = "<Product_Owner_Approved_Path>\rc-vault-20261014.vhdx"
   if (Test-Path -LiteralPath $ApprovedDestPath) {
       throw "COLLISION SECURITY ERROR: Destination file already exists. Overwrite prohibited."
   }
   Copy-Item -LiteralPath $VhdxPath -Destination $ApprovedDestPath -ErrorAction Stop
   ```

### Step 3: Post-Copy Integrity Verification
1. Compute SHA-256 hash of source `rc-vault.vhdx`:
   ```powershell
   $SourceHash = (Get-FileHash -LiteralPath $VhdxPath -Algorithm SHA256).Hash
   ```
2. Compute SHA-256 hash of copied destination `rc-vault-20261014.vhdx`:
   ```powershell
   $DestHash = (Get-FileHash -LiteralPath $ApprovedDestPath -Algorithm SHA256).Hash
   ```
3. Assert `$SourceHash -eq $DestHash`. If hashes differ, immediately delete the destination file and raise a critical transfer alert.
4. Record transfer timestamp, destination serial number, operator identity, and verified SHA-256 in the custody log.
