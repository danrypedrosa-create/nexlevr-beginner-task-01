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


### Additional screenshot evidence (captured in LetsDefend)

The screenshot of `access.log` shows example HTTP requests from `192.168.199.1` on **20 June 2021** in the lab dataset, including:

| Requested resource | HTTP status | Interpretation |
| --- | --- | --- |
| `GET /` | `200` | Root page returned successfully |
| `GET /bWAPP/` | `302` | Redirect; alone not proof of an attack |
| `GET /bWAPP/portal.php` | `200` | Portal response observed |
| `GET /bWAPP/js/html5.js` | `304` | Cache validation / not modified |
| `GET /icons/unknown.gif` | `200` | Web resource request |

The log also shows browser-like traffic with a Firefox/macOS User-Agent and referrers to `192.168.199.5`. These **specific lines** appear consistent with visiting pages and assets; they do not independently prove directory brute forcing, authentication compromise, command injection, or persistence. Additional request lines would be needed to corroborate those later events.

*Source: screenshot shared during the LetsDefend web-attack investigation. It is not yet uploaded to GitHub; screenshot upload is optional under the provided NEXLEVR requirements.*


## Verdict
**Web attack investigation challenge completed; specific exploit outcomes not independently proven by saved excerpts.** The supplied attack scenario and completion badge do not by themselves establish successful code execution, persistence, or compromise.

**Suggested action:** Preserve full logs, isolate suspect requests, analyze response patterns and payloads, and correlate with host-side evidence before assigning an outcome.

## Completion
LetsDefend **Web Attack Investigated** badge earned October 20, 2026. Raw access log not redistributed.
