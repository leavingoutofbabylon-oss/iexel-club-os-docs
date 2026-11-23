# IEXEL Club OS — Self-Hosted Scheduler Deployment Runbook (MVP)

**Document Status:** Permanent MVP Production Runbook (`SCHED-001B` accepted 2026-11-23)  
**Plugin Baseline:** `17cb2f73a83cf8e9b17ac4995f2cc76351eca839` (`feature/notify004a-adult-web-push`)

---

## 1. Purpose & Self-Hosted Architecture

IEXEL Club OS runs entirely on each club's own WordPress hosting environment with **no third-party scheduling service, paid cron SaaS, or exposed HTTP trigger URL**.

- User-initiated Event push notifications deliver immediately at PHP shutdown (`NOTIFY-007A`).
- Unattended scheduled tasks (scheduled announcements, recurring billing schedules, payment reconciliation, Back My Game tasks, and push watchdog retries) are stored in WordPress Cron and executed by the Club OS WP-CLI command:

  ```bash
  wp iexel-club-os run-scheduled
  ```

- **Important reality:** A WordPress plugin cannot wake itself up overnight with zero website traffic on its own. An operating-system-level wake-up trigger (such as one cPanel Cron Job per WordPress installation) is required for guaranteed traffic-independent execution, especially when `DISABLE_WP_CRON` is enabled or WAF rules block HTTP loopback requests to `wp-cron.php`.
- **One cPanel Cron Job per WordPress installation:** Academy and Production are completely separate WordPress installations with separate filesystem paths and MUST each have their own verified Cron Job.

---

## 2. Hosting Prerequisites

1. **cPanel Cron Jobs** (or OS `crontab`) access on the hosting account. (cPanel Terminal/SSH is helpful but **not required**.)
2. **PHP CLI >= 8.2** matching the WordPress runtime (`cli` SAPI, not `cgi-fcgi`).
3. **WP-CLI** installed on the host (commonly `/usr/bin/wp` or `/usr/local/bin/wp`).
4. **Private home directory** outside `public_html` for storing scheduler logs.

---

## 3. Identifying Paths & Verifying PHP CLI / WP-CLI Without cPanel Terminal

Many shared hosts disable cPanel Terminal. You can safely verify paths using a **temporary** cPanel Cron Job that writes to a private file outside `public_html`:

1. Identify your WordPress root directory via **cPanel → File Manager** (the folder containing `wp-config.php`, e.g. `/home/<account>/public_html/<site-dir>`).
2. Add one temporary cPanel Cron Job (set to run once in 2 minutes, then **delete immediately after inspecting the output**):
   ```bash
   (which php; /usr/local/bin/php -v; which wp; /usr/local/bin/php /usr/bin/wp --info) > /home/<account>/clubos-diag.log 2>&1
   ```
3. Inspect `/home/<account>/clubos-diag.log` via **cPanel → File Manager**, confirm:
   - PHP binary reports `(cli)` SAPI and version `8.2.x`+.
   - WP-CLI path is valid (e.g. `/usr/bin/wp`).
4. **Delete both the temporary Cron Job and `/home/<account>/clubos-diag.log` immediately.**

> **Security rule:** Never place diagnostic scripts or scheduler log files inside `public_html` or any web-accessible directory.

---

## 4. Why Direct `/usr/bin/wp` May Fail (`cgi-fcgi` SAPI) & How Explicit PHP CLI Fixes It

On many cPanel/shared hosts, invoking `/usr/bin/wp` directly uses the default `php` binary in `$PATH`, which is often the **`cgi-fcgi`** SAPI instead of **`cli`**. WP-CLI refuses to run under `cgi-fcgi` (or exits with an SAPI error).

**Resolution:** Always invoke WP-CLI explicitly through the verified PHP **CLI** binary:

```bash
<PHP_CLI_PATH> <WP_CLI_PATH> --path=<WP_ROOT_PATH> iexel-club-os run-scheduled >> <PRIVATE_LOG_PATH> 2>&1
```

---

## 5. Production Cron Job Template (Every 5 Minutes)

- **Schedule (cPanel Common Settings / Custom):** `*/5 * * * *` (every 5 minutes)
- **Reusable Production Command Template (replace placeholders with verified host paths):**

```cron
*/5 * * * * <PHP_CLI_PATH> <WP_CLI_PATH> --path=<WP_ROOT_PATH> iexel-club-os run-scheduled >> /home/<ACCOUNT_USER>/clubos-scheduler.log 2>&1
```

### Confirmed Working Academy Reference Configuration (Verified 2026-11-23)

- **Frequency:** `*/5 * * * *`
- **PHP CLI:** `/usr/local/bin/php` (PHP 8.2.36 `cli`)
- **WP-CLI:** `/usr/bin/wp`
- **WordPress root:** `/home/l69vc3oondjj/public_html/ixlfootballacademy.co.uk`
- **Private log (outside `public_html`):** `/home/l69vc3oondjj/clubos-scheduler.log`
- **Command:**
  ```cron
  */5 * * * * /usr/local/bin/php /usr/bin/wp --path=/home/l69vc3oondjj/public_html/ixlfootballacademy.co.uk iexel-club-os run-scheduled >> /home/l69vc3oondjj/clubos-scheduler.log 2>&1
  ```
- **Observed Academy results:**
  - Run 1: `5 executed` (`346ms`)
  - Run 2: `1 executed, 3 future untouched` (`55ms`)

> **Never reuse Academy paths for Production.** Verify Production's own `<PHP_CLI_PATH>`, `<WP_CLI_PATH>`, `<WP_ROOT_PATH>`, and `<ACCOUNT_USER>` independently.

---

## 6. Verification Procedure

1. **Optional dry-run first:** Temporarily append `--dry-run` to confirm due/future counts without mutating schedules, then remove `--dry-run`.
2. **Inspect the private log** (`/home/<ACCOUNT_USER>/clubos-scheduler.log` via cPanel File Manager):
   - Expect concise non-PII lines such as:
     `Success: Club OS scheduled run complete: 1 executed, 3 future untouched (55ms).`
3. **Verify repeated automatic execution:** Wait 10–15 minutes with no browser open and confirm new timestamped/success entries appear every 5 minutes.
4. **Verify due vs. future behaviour:** Confirm due Club OS tasks execute, recurring hourly jobs advance cleanly to `+1 hour` without firing every 5 minutes, and future jobs remain listed as `future untouched`.
5. **Prevent duplicate Cron Jobs:** In **cPanel → Cron Jobs**, verify there is **exactly one** `iexel-club-os run-scheduled` entry per WordPress installation. (Club OS also enforces an atomic CAS database lock `iexel_club_os_scheduled_runner_lock` + `doing_cron` coordination as defence in depth.)

---

## 7. Troubleshooting, Log Retention & Rollback

### Common Failures
- **`cgi-fcgi` / `CLI only` error:** Confirm the command begins with the explicit `cli` PHP binary (e.g. `/usr/local/bin/php`), not bare `wp` or `/usr/bin/wp`.
- **`Error: This does not seem to be a WordPress installation`:** Verify `--path=` points to the exact directory containing `wp-config.php`.
- **`Warning: Another Club OS scheduled run is already in progress; skipped.`:** Normal safety skip if a prior run is still executing; stale locks automatically expire and recover atomically after 300 seconds.
- **`Error: Club OS scheduled run finished with N failure(s)...`:** Check the named hook in PHP error logs; remaining due hooks still executed and recurring schedules were preserved.

### Log Rotation & Retention
- Because `>>` appends continuously, truncate or rotate `/home/<ACCOUNT_USER>/clubos-scheduler.log` periodically (e.g., weekly/monthly via a simple retention cron or manual truncation in File Manager), or use `>` instead of `>>` if only the latest run output is needed.
- Output contains **zero personal data, zero emails, and zero notification payloads** (counts, hook names on error, and duration in ms only).

### Rollback / Disabling
- To pause unattended execution immediately with zero plugin or database changes: **delete or comment out** the cPanel Cron Job entry.
- Existing immediate Event push (`NOTIFY-007A`) and manual admin controls remain unaffected.
