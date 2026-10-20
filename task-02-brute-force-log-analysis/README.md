# Beginner Task 02 — Linux SSH Brute-Force Log Analysis

**Program:** NEXLEVR Cybersecurity Internship — Beginner Level  
**Training source:** TryHackMe, *Log Analysis with SIEM* room (provided learning resource)  
**Tool:** Splunk Enterprise Search & Reporting (SPL)  
**Dataset:** `index=task5`, `sourcetype=linux_secure`  
**Event date in sample:** August 12, 2025  
**Evidence status:** Findings transcribed from screenshots of actual Splunk searches. Screenshot images themselves are not included in this repository yet (optional supporting proof).

## Objective

NEXLEVR Beginner Task 02 asks for an analysis of sample Windows Event Logs **or** Linux authentication logs to identify brute-force login patterns and present findings **in a table**.

This investigation analyzes SSH authentication events from the TryHackMe training dataset. The dataset is not a live customer incident.

## Methodology

1. Discovered available indexes and sourcetypes with:
   ```spl
   | tstats count WHERE index=* BY index sourcetype
   ```
   The environment returned four sourcetype groups totaling **2,238 events**. The Linux authentication subset was `task5/linux_secure`, containing **62 events**.

2. Reviewed raw authentication records:
   ```spl
   index=task5 sourcetype=linux_secure
   | table _time host _raw
   | head 15
   ```

3. Searched for authentication failures:
   ```spl
   index=task5 sourcetype=linux_secure ("Failed password" OR "Invalid user" OR "authentication failure")
   | table _time host _raw
   | sort 0 _time
   ```
   This returned **7 matching log events**, including PAM authentication-failure messages and a syslog-compressed `message repeated 2 times` entry.

4. Counted actual `Failed password` attempts, accounting for the compressed repeat record:
   ```spl
   index=task5 sourcetype=linux_secure "Failed password"
   | rex field=_raw "Failed password for (?<username>\S+) from (?<source_ip>\d{1,3}(?:\.\d{1,3}){3})"
   | rex field=_raw "message repeated (?<repetitions>\d+) times"
   | eval attempts=if(isnotnull(repetitions),tonumber(repetitions),1)
   | stats sum(attempts) as failed_attempts by source_ip username
   | sort - failed_attempts
   ```
   Result: **5 matched event records**, representing **6 failed password attempts** to `jack-brown`.

5. Correlated accepted logins:
   ```spl
   index=task5 sourcetype=linux_secure "Accepted password"
   | table _time host _raw
   | sort 0 _time
   ```
   Result: **4 successful SSH logins**.

6. Built the final comparison table:
   ```spl
   index=task5 sourcetype=linux_secure ("Failed password" OR "Accepted password")
   | rex field=_raw "(?:Failed|Accepted) password for (?<username>\S+) from (?<source_ip>\d{1,3}(?:\.\d{1,3}){3})"
   | rex field=_raw "message repeated (?<repetitions>\d+) times"
   | eval failed=if(match(_raw,"Failed password"),coalesce(tonumber(repetitions),1),0)
   | eval successful=if(match(_raw,"Accepted password"),1,0)
   | stats sum(failed) as failed_attempts sum(successful) as successful_logins by source_ip username
   | sort - failed_attempts
   ```
   Result: **9 matched log records** (5 `Failed password` records and 4 `Accepted password` records).

## Findings table

| Source IP | Username | Failed password attempts | Successful SSH logins | Assessment |
| --- | --- | ---: | ---: | --- |
| `10.14.94.82` | `jack-brown` | **6** | **1** | Repeated failures followed by success; suspicious for password guessing |
| `10.14.94.82` | `ubuntu` | 0 | **3** | Successful sessions recorded; no failed passwords for this account within the query results |
| **Total** | | **6** | **4** | One source IP in these matching events |

**Notes about counting:** A syslog event containing `message repeated 2 times` represents two failures. The PAM `authentication failure` entries were **not** added to the password failure count because that could double-count the same authentication attempts. Counts are limited to this dataset, time range, and query terms.

## Timeline of notable events (2025-08-12, UTC)

| Timestamp | Observation |
| --- | --- |
| 09:50:25 | PAM authentication failure for `jack-brown` |
| 09:50:27 | Failed SSH password for `jack-brown` from `10.14.94.82` |
| 09:50:36 | Log entry reporting an earlier password failure message repeated twice |
| 09:51:00 | Last visible failed password for `jack-brown` |
| 09:51:29 | **Accepted password** for `jack-brown` from the same source IP |
| 09:53:51, 09:53:59, 09:54:13 | Accepted SSH logins for `ubuntu` from the same source IP |

The accepted `jack-brown` login was approximately **29.7 seconds** after the last recorded failed attempt.

## Verdict

**Suspicious SSH authentication sequence consistent with possible brute-force/password-guessing followed by a successful login.**

The same source IP (`10.14.94.82`) generated **six failed password attempts** for `jack-brown` and then **one accepted password** for that account. This warrants investigation, but the logs **do not establish** whether the source was unauthorized or the credentials were compromised. `10.14.94.82` is a private network IP in the training environment.

**Recommended SOC response:** Verify account ownership and expected access, correlate with SSH server session/activity logs and source-device records, review any post-login actions, and consider hardening controls (MFA where supported, strong passwords/keys, login throttling and alerting).

## Evidence reference

Screenshots captured during the TryHackMe/Splunk lab were named for local organization:

- `01-linux-authentication-logs.png` — 62-event authentication log overview
- `02-failed-ssh-login-attempts.png` — 7 authentication-failure-related records
- `03-failed-login-counts.png` — 6 failed password attempts, grouped by source IP and username
- `04-successful-ssh-logins.png` — 4 accepted password events
- `05-final-authentication-analysis.png` — combined failed/successful results

These are **optional evidence screenshots**, not a NEXLEVR-mandated screenshot count. They have not yet been uploaded to this repository.

## Limitations

- Findings are based on the provided TryHackMe dataset, not real-world systems.
- The screenshot evidence establishes event strings and query outputs, not authorization context.
- Successful SSH authentication does not by itself prove a malicious compromise.
