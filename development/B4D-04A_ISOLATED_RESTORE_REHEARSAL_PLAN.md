# B4D-04A Isolated Restore Rehearsal Plan (Revision 2)
**Document Reference:** `B4D-04A-DOC-03-R2`  
**Classification:** Restricted Rehearsal Specification  
**System:** IEXEL Club OS (Grassroots Football Club Management)  
**Authoritative Baselining:** Commit `452b30312dcc16ad3b1c6c7d0d74503b27c5c9bc`  
**Synthetics Baseline:** 117 Passing Synthetic Unit & Security Tests  
**Operational Status:** Read-Only Specification — Rehearsal Prohibited Pending Gate E Approval  

---

## 1. Executive Summary & Purpose

A backup that has never been restored is an unverified hypothesis. The purpose of this **Isolated Restore Rehearsal Plan** is to define a non-destructive, repeatable rehearsal drill for any candidate encrypted backup package created by `Invoke-ClubOsBackupPackaging.ps1`.

### Mandatory Operational Boundaries:
1. **Rehearsal is Strictly Prohibited Pending Gate E:** Mounting candidate backup volumes and extracting contents for restore verification requires formal sign-off from the Product Owner under **Approval Gate E** as a separate, dedicated execution batch (B4D-04E).
2. **Absolute Fleet Isolation:** The rehearsal environment must be physically and logically air-gapped from live development (`iexel-club-os-dev` on port 10012), Release Candidate Clean (`iexel-rc-clean` on port 10009), and Release Candidate Upgrade (`iexel-rc-upgrade`).
3. **Dedicated Disposable Database Service:** The rehearsal drill **must not** reuse the host LocalWP MySQL instance or merely provision an extra schema on a shared port. It requires a dedicated, ephemeral, disposable database service (e.g., an isolated container or temporary standalone MySQL daemon) bound to a dynamically verified free port.
4. **OS-Level Network Egress Blocking:** Restored application code must be blocked from outbound network communication at the OS / firewall / container boundary prior to bootstrap.
5. **Safeguarding Data Minimisation:** Verification queries must inspect table schemas, record counts, and structural indexes without outputting or logging youth player, guardian, medical, or safeguarding Personal Identifiable Information (PII) to consoles, evidence transcripts, or disk traces.
6. **Teardown Ownership & Prevention of Unsafe Cleanup (Correction C):** Rigorous creation-time ownership records, unique run identifiers, and exact identity checks must be verified before stopping, dropping, or removing any rehearsal resource.

---

## 2. Authoritative Manifest Contract & Table-Count Property Path (Correction C)

The rehearsal drill consumes the exact five standard artifacts produced by the committed backup script (`Invoke-ClubOsBackupPackaging.ps1`) inside the root of the mounted `IEXEL_RC_VAULT` BitLocker volume:

| Artifact Name | Description & Verification Method |
|---|---|
| `database.sql` | Plaintext SQL dump (protected at rest by BitLocker). Verified via `-- Dump completed on YYYY-MM-DD` tail marker. |
| `files.zip` | ZIP archive of the WordPress filesystem. Verified via ZIP directory entry count and absence of ZipSlip patterns. |
| `IEXEL_BACKUP_MANIFEST.json` | Authoritative JSON manifest containing source site identity, file SHA-256 hashes, and verified database table count. |
| `PROVENANCE.json` | Companion JSON document capturing Git HEAD (`452b30312dcc16ad3b1c6c7d0d74503b27c5c9bc`), tracked tree status, and WP/PHP/MySQL versions. |
| `CHECKSUMS.sha256` | Standard Unix-format hash file containing SHA-256 checksums of the above four artifacts. |

### Verified Manifest Table-Count Property Path
Inspection of the authoritative committed backup script `tools/backup/Invoke-ClubOsBackupPackaging.ps1` confirms the exact schema structure of `IEXEL_BACKUP_MANIFEST.json`:

- **Code Location 1 (`New-BackupManifestDocument`, lines 2034–2039):**
  ```powershell
  Database = [ordered]@{
      FileName     = $DumpFileName
      FileSizeBytes= $DumpFileBytes
      Sha256       = $DumpFileSha256
      TableCount   = $DumpTableCount
  }
  ```
- **Code Location 2 (`Invoke-BackupExecutionPipelineInternal`, lines 2496–2509):**
  `-DumpTableCount $dumpIntegrity.TableCount` passed directly into `Database.TableCount`.
- **Secondary Identity Record (lines 2028 & 1220):**
  Also mirrored in `$Manifest.SourceIdentity.TableCount`.

> **Authoritative Property Path:** The primary and authoritative property path for the verified database table count in `IEXEL_BACKUP_MANIFEST.json` is:  
> **`$Manifest.Database.TableCount`**  
> All rehearsal schema parity checks must evaluate against this exact property path.

---

## 3. Rehearsal Environment Architecture & Isolation Controls

```
+---------------------------------------------------------------------------------------------------------+
| HOST WORKSTATION (Windows 11)                                                                           |
|                                                                                                         |
|  [ PROTECTED LIVE FLEET - ZERO TOUCH / ZERO COLLISION ]                                                 |
|  - Dev Site:      127.0.0.1:10012 | Schema: local | Path: Local Sites\iexel-club-os-dev                |
|  - RC Clean:      127.0.0.1:10009 | Schema: local | Path: Local Sites\iexel-rc-clean                   |
|  - RC Upgrade:    LocalWP Fleet Container                                                               |
|                                                                                                         |
|  ================================ OS / FIREWALL EGRESS BARRIER ======================================== |
|                                                                                                         |
|  [ RESTORE DRILL SANDBOX (Disposable Ephemeral Instance) ]                                              |
|  Sandbox Root: C:\Users\leavi\.codex\restore-sandboxes\drill-[RunId]\                                    |
|                                                                                                         |
|  +-------------------------------------+   +---------------------------------------------------------+  |
|  | Dedicated Disposable Database        |   | Restored Application Filesystem                         |  |
|  | - Standalone disposable daemon/PID  |   | - Extracted from `files.zip` into ephemeral sandbox     |  |
|  | - Port: Dynamically verified free   |   | - Egress: Blocked at OS/Firewall level                  |  |
|  | - Schema: `drill_restore_[RunId]`   |   | - Defense-in-depth: WP_HTTP_BLOCK_EXTERNAL = true       |  |
|  | - Parity Target: Manifest TableCount|   | - Mail: pre_wp_mail intercepted and discarded           |  |
|  +-------------------------------------+   +---------------------------------------------------------+  |
+---------------------------------------------------------------------------------------------------------+
```

### 3.1 Strict Isolation Guardrails
1. **Dynamic Port Verification:** The drill must not assume port 10015 or any fixed port is free. The execution harness must dynamically test candidate ports (`Test-NetConnection -ComputerName 127.0.0.1 -Port $CandidatePort`) to confirm zero listeners exist before binding the disposable database service.
2. **Dedicated Disposable Database Service:** The drill must instantiate an isolated, temporary MySQL daemon process or disposable container. Reusing LocalWP MySQL instances (e.g., ports 10012, 10009) is strictly forbidden to prevent accidental cross-schema contamination or service interruption.
3. **OS-Level Network Egress Blocking:** Prior to booting WordPress or running CLI commands against the restored files, outbound traffic must be denied at the OS or container boundary (e.g., dedicated Windows Firewall outbound block rule applied to the PHP executable path or container loopback-only network namespace).
4. **Application-Level Defense-in-Depth:** In addition to OS-level blocking, the sandbox `wp-config.php` must inject:
   ```php
   define( 'WP_HTTP_BLOCK_EXTERNAL', true );
   define( 'WP_ACCESSIBLE_HOSTS', '127.0.0.1,localhost' );
   define( 'AUTOMATIC_UPDATER_DISABLED', true );
   define( 'DISABLE_WP_CRON', true );
   ```
   Mail routing must be intercepted via `add_filter('pre_wp_mail', '__return_true');` to ensure no live emails can be sent to players, parents, or staff.
5. **Path Canonicalization & Non-Overlap Proof:** The sandbox path must be generated using `[Guid]::NewGuid().ToString("N")` under `$env:USERPROFILE\.codex\restore-sandboxes\`. The harness must prove via `Assert-CanonicalPathContainment` that the sandbox path is completely disjoint from `c:\Users\leavi\Local Sites`.

---

## 4. Step-by-Step Rehearsal Protocol (PROHIBITED PENDING GATE E)

> [!CAUTION]
> **OPERATIONAL GATE E REQUIRED:** The following steps require explicit authorization from the Product Owner under a dedicated batch (B4D-04E) and must be conducted under active human operator supervision.

### Step 1: Preflight Verification & Vault Mounting
1. Generate unique execution identifier:
   `$RunId = [Guid]::NewGuid().ToString('N')`
   `$RunToken = "drill-" + (Get-Date -Format "yyyyMMdd-HHmmss") + "-" + $RunId`
2. Initialize in-process rehearsal tracker registering all intended resource identities.
3. Attach BitLocker VHDX container in **Read-Only** mode:
   ```powershell
   # PROHIBITED PENDING FORMAL GATE E APPROVAL
   $VhdxPath = "C:\Users\leavi\.codex\private-backups\iexel-rc-VYqEpdwXa\rc-vault.vhdx"
   Mount-DiskImage -ImagePath $VhdxPath -StorageType VHDX -AccessMode ReadOnly
   ```
4. Interactively unlock BitLocker volume; verify volume label `IEXEL_RC_VAULT`.
5. Validate storage re-read integrity using `CHECKSUMS.sha256`.
6. Read `IEXEL_BACKUP_MANIFEST.json` and extract the authoritative expected table count:
   ```powershell
   $Manifest = Get-Content -LiteralPath (Join-Path $VaultDrive "IEXEL_BACKUP_MANIFEST.json") | ConvertFrom-Json
   $ExpectedTableCount = [int]$Manifest.Database.TableCount
   ```

### Step 2: Sandbox Provisioning & Payload Extraction
1. Create unique sandbox directory with restrictive ACLs:
   `$SandboxPath = Join-Path $env:USERPROFILE ".codex\restore-sandboxes\$RunToken"`
   Register `$SandboxPath` in the rehearsal tracker.
2. Unpack `files.zip` into `$SandboxPath\wordpress\`. Verify total extracted file count and absence of path traversal indicators.
3. Configure `wp-config.php` with sandbox connection strings and mandatory defense-in-depth egress blocks.

### Step 3: Dedicated Disposable Database Startup & Ingestion
1. Start dedicated disposable database daemon on a verified unused local port. Record its Process ID (PID), port, and temporary data directory in the tracker.
2. Generate secure temporary `my.cnf` defaults-file in the sandbox with restrictive owner ACLs (no passwords passed via command-line parameters).
3. Create drill schema:
   `$DrillDbName = "drill_restore_$RunId"`
   `CREATE DATABASE $DrillDbName CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_520_ci;`
   Register `$DrillDbName` in the tracker.
4. Ingest `database.sql` into `$DrillDbName` using `--defaults-extra-file`.
5. Securely wipe the temporary `my.cnf` defaults-file immediately upon ingestion.

### Step 4: Database Schema Parity Verification
1. Query table count on `$DrillDbName`:
   ```sql
   SELECT COUNT(*) FROM information_schema.tables WHERE table_schema = '$DrillDbName';
   ```
2. **Authoritative Parity Criterion:** Restored table count must match `$Manifest.Database.TableCount` exactly:
   `Assert-True ($RestoredTableCount -eq $ExpectedTableCount)`
3. Validate presence of core WordPress tables and all custom Club OS tables (`wp_clubos_*`).

### Step 5: Headless WordPress Boot & Domain Sanity Checks
1. Execute headless boot check using WP-CLI configured against the sandbox path:
   ```powershell
   wp core is-installed --path="$SandboxPath\wordpress"
   ```
2. Verify active status of `iexel-club-os` plugin:
   ```powershell
   wp plugin is-active iexel-club-os --path="$SandboxPath\wordpress"
   ```
3. **Core Football Domain Structural Smoke Tests (Read-Only):**
   - **Player Registrations:** Query `wp_posts` / `wp_postmeta` to verify player registration records and FA affiliation metadata exist structurally.
   - **Memberships & Subscriptions:** Verify subscription ledger rows, fee category links, and payment method tokens exist structurally.
   - **Safeguarding & Medical Emergency Alerts:** Verify safeguarding case schemas and emergency contact metadata structures are intact.
   - **Audit Logs:** Confirm `wp_clubos_audit_log` records are preserved and readable up to the recorded quiescence checkpoint.

### Step 6: Safeguarding & Sensitive Data Minimisation Audit
1. **PII Redaction Assertion:** Confirm that no youth player names, dates of birth, home addresses, guardian phone numbers, or medical free-text notes appear in console logs, terminal scrollback, or test reports.
2. **Application Encryption Verification:** Confirm that fields designated for application-level encryption at rest remain stored as ciphertext in the restored database.

---

## 5. Teardown Ownership & Prevention of Unsafe Cleanup (Correction C)

The operator and harness must execute rigorous identity and ownership verification before deleting, stopping, or dismantling any resource.

### 5.1 Pre-Teardown Identity & Ownership Verification
Before executing any destructive disposal commands:
1. **Unique Run Identifier Check:** Verify that the resource's recorded metadata contains the active `$RunToken` and `$RunId`.
2. **Creation-Time Ownership Record:** Confirm that the resource is explicitly listed in the in-process rehearsal tracker.
3. **Exact Target Identity Checks:**
   - **Database Daemon:** Verify that the running process matches the exact recorded PID and that its command line points strictly to the sandbox data directory.
   - **Database Schema:** Verify that the schema name is exactly `$DrillDbName` (`drill_restore_$RunId`) and that the connection port is the disposable daemon port (never 10012, 10009, or live ports).
   - **Filesystem Sandbox:** Verify that `$SandboxPath` canonicalizes strictly under `$env:USERPROFILE\.codex\restore-sandboxes\` and passes `Assert-CanonicalPathContainment`.
   - **Firewall Rules:** Verify that the temporary firewall rule contains the exact rule name `ClubOs_Drill_Block_$RunId` and was created during this run.
4. **Protection of Pre-Existing Resources:** Resources that existed prior to rehearsal execution (or that lack positive creation ownership records) must **NEVER** be deleted or modified.
5. **Failure Handling & Operator Escalation:** If ownership cannot be established with 100% certainty for any resource, **HALT TEARDOWN IMMEDIATELY**. Do not fall back to fuzzy, wildcard, or name-based deletes. Escalate to the human operator for manual inspection.

### 5.2 Safe Teardown Execution
If and only if all ownership checks pass:
1. **Stop & Dismantle Disposable Database:**
   - Terminate the verified disposable MySQL daemon PID.
   - Remove the temporary disposable database directory.
2. **Restore Pre-Existing Firewall State:**
   - Remove strictly the verified rule `ClubOs_Drill_Block_$RunId`.
   - Verify that all pre-existing system firewall rules remain intact.
3. **Dismount & Lock Vault Container:**
   ```powershell
   # PROHIBITED PENDING FORMAL GATE E APPROVAL
   Lock-BitLocker -MountPoint "<Assigned_Vault_Drive_Letter>:" -ForceDismount
   Dismount-DiskImage -ImagePath $VhdxPath
   ```
4. **Sandbox Directory Removal:**
   - Remove `$SandboxPath` using standard recursive filesystem deletion (`Remove-Item -LiteralPath $SandboxPath -Recurse -Force`).

---

## 6. Rehearsal Pass/Fail Criteria Checklist

| ID | Checkpoint | Authoritative Pass Standard | Verification Status |
|---|---|---|---|
| **RPC-01** | Manifest Storage Checksum | Bit-for-bit match of `database.sql`, `files.zip`, `PROVENANCE.json`, `IEXEL_BACKUP_MANIFEST.json` against `CHECKSUMS.sha256`. | `[ ] PENDING GATE E` |
| **RPC-02** | Sandbox Directory Isolation | Restored files contained entirely within ephemeral UUID sandbox; zero collision with live sites. | `[ ] PENDING GATE E` |
| **RPC-03** | Dedicated Database Service | Dedicated disposable database service on dynamically verified port; zero shared LocalWP DB usage. | `[ ] PENDING GATE E` |
| **RPC-04** | OS & App Egress Denial | OS-level network block active; zero outbound sockets permitted; `pre_wp_mail` suppression active. | `[ ] PENDING GATE E` |
| **RPC-05** | Credential Security | Zero plaintext passwords passed via CLI arguments; temporary `my.cnf` securely removed. | `[ ] PENDING GATE E` |
| **RPC-06** | Schema Parity | Table count on restored schema exactly equals `$Manifest.Database.TableCount`. | `[ ] PENDING GATE E` |
| **RPC-07** | Application Boot | Headless WP-CLI reports WordPress installed and `iexel-club-os` plugin active without fatal errors. | `[ ] PENDING GATE E` |
| **RPC-08** | Football Domain Sanity | Players, registrations, memberships, and audit log structures verified intact. | `[ ] PENDING GATE E` |
| **RPC-09** | Safeguarding Data Protection | Zero PII leaked to logs or console; encrypted fields verified as ciphertext at rest. | `[ ] PENDING GATE E` |
| **RPC-10** | Teardown Ownership & Safety | Positive token/PID ownership verified before disposal; zero pre-existing resources touched; sandbox removed. | `[ ] PENDING GATE E` |
