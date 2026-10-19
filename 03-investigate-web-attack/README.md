# Lab 03 — Investigate Web Attack

**Platform:** LetsDefend | **Completed:** October 20, 2026 | **Badge:** Web Attack Investigated

## Alert / Scenario
A LetsDefend training challenge supplied an Apache-style `access.log` file for investigating web reconnaissance, directory discovery, further attack activity, and possible persistence-related requests against a bWAPP test application.

## Evidence
A retained screenshot showed an initial set of web requests:
- Visible client **`192.168.199.1`** requesting `/`, `/bWAPP/`, `/bWAPP/portal.php`, and static resources.
- HTTP statuses included `200`, `302`, and `304`.
- The first visible requests had a Firefox/macOS User-Agent.
- These opening log lines alone are **not proof of exploitation**.

**Investigation method:** Opened `access.log` inside the Linux VM. The intended read-only review commands include:

```bash
cd /root/Desktop/ChallengeFile
ls -lh
grep -Ei 'nikto|dirb|gobuster|dirbuster|ffuf|wfuzz' access.log | head -n 30
awk -F'"' '{print $6}' access.log | sort | uniq -c | sort -nr | head -20
grep '/bWAPP/' access.log | head -n 30
```

The challenge asked about later attack types, payloads, and persistence clues; however, screenshots preserving those specific log requests and responses were not retained.

## Verdict
**Web attack investigation challenge completed; specific exploit outcomes not independently proven by saved excerpts.** The supplied attack scenario and completion badge do not by themselves establish successful code execution, persistence, or compromise.

**Suggested action:** Preserve full logs, isolate suspect requests, analyze response patterns and payloads, and correlate with host-side evidence before assigning an outcome.

## Completion
LetsDefend **Web Attack Investigated** badge earned October 20, 2026. Raw access log not redistributed.
