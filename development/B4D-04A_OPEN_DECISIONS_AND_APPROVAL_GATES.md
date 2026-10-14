# B4D-04A Open Decisions and Approval Gates (Revision 2)
**Document Reference:** `B4D-04A-DOC-04-R2`  
**Classification:** Product Governance & Operational Decision Framework  
**System:** IEXEL Club OS (Grassroots Football Club Management)  
**Authoritative Baselining:** Commit `452b30312dcc16ad3b1c6c7d0d74503b27c5c9bc`  
**Synthetics Baseline:** 117 Passing Synthetic Unit & Security Tests  
**Operational Status:** Governance Framework — Separate Authorization Required for Every Gate  

---

## 1. Executive Summary & Governance Model

The technical packaging logic for IEXEL Club OS has achieved **117 passing synthetic unit and security tests** in commit `452b30312dcc16ad3b1c6c7d0d74503b27c5c9bc`. However, the execution mode of the backup tooling remains unconditionally blocked in code, and neither live backup execution nor live restore has yet occurred.

To transition responsibly from read-only planning to live operational execution, this document establishes:
1. **Six Separate, Non-Combined Operational Approval Gates (Gates A through F):** Each gate represents an independent authorization boundary requiring explicit Product Owner sign-off before any action is undertaken. Under no circumstances may Gates B through E be merged into a single execution batch.
2. **Authoritative Manifest Parity Reference:** Formal definition of the verified manifest property path **`Database.TableCount`** for Gate E verification, matching the committed code contract in `tools/backup/Invoke-ClubOsBackupPackaging.ps1`.
3. **Five Open Architectural & Operational Decisions:** Key governance, business continuity, retention, and storage parameters that must be determined by the Product Owner rather than assumed by engineering.

---

## 2. Separate Product Owner Approval Gates (Gates A – F)

Every transition in the disaster recovery verification lifecycle requires an independent, written authorization from the Product Owner. Gates must be evaluated and approved sequentially.

```
+----------------------------------------------------------------------------------------------------+
| STRICT SEQUENTIAL APPROVAL GATES (ZERO BATCH COMBINATION)                                          |
|                                                                                                    |
|  [GATE A] Planning & Runbook Acceptance (READ-ONLY)                                                |
|     * Review and acceptance of Docs 01, 02, 03, 04 (Revision 2).                                   |
|     * Does NOT authorize live execution, maintenance mode, or vault mounting.                     |
|     v                                                                                              |
|  [GATE B] Quiescence & Maintenance Mode Authorization (BATCH B4D-04B)                             |
|     * Authorizes scheduled read-only maintenance window and worker process suspension.             |
|     * Requires explicit pre-existing state recording, ownership token, and rollback plan.          |
|     v                                                                                              |
|  [GATE C] Supervised Live Backup Execution Authorization (BATCH B4D-04C)                          |
|     * Authorizes dedicated, peer-reviewed engineering batch to lift Execution blocker.             |
|     * Authorizes human-supervised packaging into pre-attached BitLocker vault.                     |
|     v                                                                                              |
|  [GATE D] Off-Device Custody & Secondary Storage Confirmation (BATCH B4D-04D)                     |
|     * Authorizes replication of encrypted VHDX to approved external secondary destination.         |
|     * Requires capacity check, collision prevention, and post-copy SHA-256 verification.           |
|     v                                                                                              |
|  [GATE E] Isolated Restore Rehearsal Authorization (BATCH B4D-04E)                                 |
|     * Authorizes non-destructive restore drill in dedicated disposable database sandbox.           |
|     * Requires OS egress denial, schema parity against $Manifest.Database.TableCount, smoke tests. |
|     * Enforces creation-time ownership verification before teardown.                               |
|     v                                                                                              |
|  [GATE F] Disaster Recovery Evidence Acceptance (GOVERNANCE ACCEPTANCE)                            |
|     * Formal acceptance of demonstrated recovery evidence.                                         |
|     * NOTE: Does NOT constitute automatic Club OS production release approval.                     |
+----------------------------------------------------------------------------------------------------+
```

### Detailed Gate Specifications

| Gate ID | Scope & Purpose | Required Preconditions | Verification Deliverables | Sign-Off Authority |
|---|---|---|---|---|
| **Gate A** | **Planning & Runbook Acceptance:** Formal sign-off on the revised B4D-04A recovery assessment, runbook, rehearsal plan, and decision framework. | Zero state modifications; 117 synthetic tests confirmed passing; clean Git baseline. | Accepted B4D-04A (R2) documentation set. | Product Owner |
| **Gate B** | **Quiescence & Maintenance Authorization (Batch B4D-04B):** Authorize placing target development environment into maintenance mode and suspending workers. | Gate A passed; operational maintenance window scheduled; pre-existing maintenance state recorded. | Execution log verifying `.maintenance` active with unique token, workers paused, 0 non-sleep queries. | Product Owner |
| **Gate C** | **Supervised Backup Authorization (Batch B4D-04C):** Authorize dedicated engineering batch to enable Execution mode and execute live packaging. | Gate B passed; BitLocker VHDX attached; destination empty of prior packages; operator present. | Pipeline execution transcript; vault output matching 5-artifact contract; SHA-256 match. | Product Owner |
| **Gate D** | **Off-Device Custody Confirmation (Batch B4D-04D):** Authorize and verify replication of encrypted container to approved external secondary storage. | Gate C passed; vault locked and dismounted; destination path approved; collision check passed. | Custody transfer log; bit-for-bit source and destination SHA-256 verification report. | Product Owner & Security Lead |
| **Gate E** | **Isolated Restore Rehearsal Authorization (Batch B4D-04E):** Authorize mounting candidate backup and executing non-destructive drill in disposable sandbox. | Gate D passed; disposable sandbox initialized; dedicated DB service provisioned; OS egress blocked. | Rehearsal drill report verifying schema parity (`$Manifest.Database.TableCount`), domain sanity, safe teardown. | Product Owner |
| **Gate F** | **DR Evidence Acceptance (Batch B4D-04F):** Formal recognition that the disaster recovery procedure has been proven viable and repeatable. | Gate E passed with zero critical anomalies; all transient sandboxes wiped clean with verified ownership. | Signed DR Closure Report. *(Does NOT grant automatic release approval for Club OS).* | Product Owner |

---

## 3. Verified Manifest Table-Count Parity Path

In accordance with Section 4 of the B4D-04A-R2 specification, the property path used for database table count parity checking during Gate E verification is explicitly established from the committed code in `tools/backup/Invoke-ClubOsBackupPackaging.ps1`:

- **Code Location:** `New-BackupManifestDocument` (lines 2034–2039) defines:
  ```powershell
  Database = [ordered]@{
      FileName     = $DumpFileName
      FileSizeBytes= $DumpFileBytes
      Sha256       = $DumpFileSha256
      TableCount   = $DumpTableCount
  }
  ```
- **Authoritative Manifest Path:**
  **`$Manifest.Database.TableCount`**
- **Secondary Identity Mirror:**
  `$Manifest.SourceIdentity.TableCount` (lines 2028 & 1220).

Gate E parity verification must assert that the restored schema table count matches `$Manifest.Database.TableCount` bit-for-bit, rather than using an arbitrary hardcoded number.

---

## 4. Open Architectural & Operational Decisions

The following five strategic decisions require formal determination by the Product Owner:

### Decision 1: RPO (Recovery Point Objective) & RTO (Recovery Time Objective) Targets
* **Context:** Recovery targets must balance data freshness against operational overhead and technical complexity in grassroots football operations.
* **Trade-Off Analysis:**
  - *RPO Considerations:* Player registrations, team sheets, match results, and fee payments occur intermittently during weekdays and heavily on match weekends. An RPO of 24 hours (daily quiesced backup) is straightforward but risks losing a full day's registrations during peak registration windows. An RPO of 1–4 hours requires continuous automated background exports or transaction-log replication, introducing significant operational complexity.
  - *RTO Considerations:* An RTO cannot be assumed or established as "4 hours" prior to live testing. RTO depends entirely on the size of the database dump, file archive extraction speed, hardware performance, and operator availability. Live rehearsal data from Gate E will be required to establish realistic baseline RTO metrics.
* **Open Decision for Product Owner:** Define acceptable business loss tolerances (RPO) and operational restoration time targets (RTO) for grassroots club operations.

### Decision 2: Off-Device Secondary Storage Architecture & Destination
* **Context:** The candidate encrypted vault (`rc-vault.vhdx`) currently resides on `C:\Users\leavi\.codex\private-backups\`, sharing the same physical NVMe SSD as the host OS and LocalWP installations. A physical drive failure or BitLocker volume header corruption on `C:` would destroy both primary data and backup.
* **Architectural Options for Resolution:**
  - *Option 2A (Air-Gapped Hardware Encrypted Removable Media):* Dedicated external SSD or USB drive encrypted via BitLocker To Go or hardware PIN keypad, stored in a physical fireproof container.
  - *Option 2B (Cloud Object Storage with Immutability):* Automated transfer to an isolated AWS S3 bucket or Azure Blob Container configured with Object Lock (WORM - Write Once Read Many) and customer-managed KMS key encryption.
  - *Option 2C (Isolated Network Storage):* Dedicated encrypted NAS share physically separate from the primary development workstation subnet.
* **Open Decision for Product Owner:** Formally designate and approve the physical secondary destination path, hardware medium, and transfer mechanism.

### Decision 3: BitLocker Recovery Key Escrow Policy & Custody Model
* **Context:** The BitLocker 48-digit numerical recovery key and volume passphrase for `IEXEL_RC_VAULT` must be securely escrowed to prevent permanent data lock-out while maintaining strict confidentiality against unauthorized access.
* **Custody Models for Resolution:**
  - *Option 3A (Dual-Custody Split Secret):* Recovery key is split or stored in an enterprise password manager (e.g., 1Password / Bitwarden Enterprise) requiring dual-operator approval to view.
  - *Option 3B (Physical Air-Gapped Safe):* Key is printed, placed in a tamper-evident sealed envelope, and deposited in an off-site physical secure safe.
  - *Option 3C (Hardware Security Module / Cloud Key Vault):* Automated key escrow via Azure Key Vault or AWS KMS with restricted IAM role policies and audit logging.
* **Open Decision for Product Owner:** Formally designate the primary and secondary key custody holders and the authorized retrieval protocol.

### Decision 4: Restore Rehearsal Target Environment Footprint
* **Context:** Verifying restore viability requires an isolated target environment that cannot collide with or contaminate active LocalWP instances (Dev on 10012, RC Clean on 10009, RC Upgrade).
* **Environment Models for Resolution:**
  - *Option 4A (Ephemeral Disposable Container / Standalone Daemon):* On-demand temporary directory with a dedicated, isolated MySQL process bound to a dynamically verified free port, destroyed immediately upon drill completion.
  - *Option 4B (Dedicated Permanent Staging Infrastructure):* Provision a separate, permanently isolated staging host dedicated exclusively to periodic recovery rehearsal testing.
* **Open Decision for Product Owner:** Approve whether rehearsal drills occur in ephemeral disposable sandboxes (Option 4A) or dedicated permanent staging environments (Option 4B).

### Decision 5: Backup Cadence & Data Retention Lifecycle Policy
* **Context:** Retention policies must balance regulatory compliance (UK GDPR, FA Safeguarding Regulations, statutory accounting rules) against storage costs and data minimisation principles.
* **Policy Nuance:**
  - **Statutory Financial Records:** Statutory tax and fiscal accounting records (e.g., membership fee invoices, HMRC Gift Aid ledgers) may require statutory retention periods (up to 6–7 years).
  - **General Operational Backups & Youth Member Data:** Operational database snapshots containing youth player medical alerts, emergency guardian contacts, and scouting notes must adhere to **GDPR Data Minimisation (Article 5(1)(e))**. Retaining full operational database backups containing transient youth member data for 7 years is legally problematic and excessive.
* **Proposed Tiered Retention Model:**
  - *Operational Daily Snapshots:* Retained for 7 to 14 days, then deleted.
  - *Operational Weekly Snapshots:* Retained for 4 weeks, then deleted.
  - *Monthly Milestone Snapshots:* Retained for 3 to 6 months.
  - *Annual Fiscal Audit Checkpoints:* Financial ledgers extracted and archived separately under statutory accounting retention rules (up to 7 years) with sensitive youth player medical/safeguarding notes sanitized or redacted.
* **Open Decision for Product Owner:** Ratify the tiered backup cadence and data retention schedule, confirming distinct treatment for operational youth data vs. statutory financial audit archives.

---

## 5. Next Controlled Batches Progression

Progression follows strict sequential batches upon Gate A sign-off:
- **Batch B4D-04B:** Operator Quiescence Protocol (Gate B).
- **Batch B4D-04C:** Supervised Backup Execution & Verification (Gate C).
- **Batch B4D-04D:** Off-Device Replication & Custody Verification (Gate D).
- **Batch B4D-04E:** Isolated Restore Rehearsal in Disposable Sandbox (Gate E).
- **Batch B4D-04F:** DR Evidence Evaluation & Closure (Gate F).
