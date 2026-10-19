# SOC Investigation Labs | NEXLEVR Beginner Task 01

**Three completed LetsDefend training investigations** covering phishing email analysis, TCP port-scanning traffic, and web-server access logs. Prepared as proof of work for the NEXLEVR Cybersecurity Internship (Beginner Level, Task 01).

> **Status:** 3/3 LetsDefend challenges completed. Write-ups and completion evidence included. **NEXLEVR verification is pending**; this repository does not represent an internship certificate or professional certification.

## Investigations

| Lab | Scenario | Analysis tools | Verdict | Completion |
| --- | --- | --- | --- | --- |
| [01 — Phishing Email](01-phishing-email/README.md) | PayPal-themed German-language email | Thunderbird, raw headers, URL inspection | Likely phishing; compromise not established | Oct 19, 2026 · Phishing Analyzer |
| [02 — Port Scan Activity](02-port-scan-activity/README.md) | Repeated TCP SYN requests targeting multiple hosts and ports | Wireshark, PCAP analysis, protocol filters | Port-scanning behavior observed; no proven intrusion | Oct 19, 2026 · Detector |
| [03 — Investigate Web Attack](03-investigate-web-attack/README.md) | Review web-server requests in a bWAPP lab | Linux, Apache access log review | Lab completed; detailed exploit outcome cannot be independently validated from retained screenshots | Oct 20, 2026 · Web Attack Investigated |

## Task requirement

NEXLEVR asks Beginner Task 01 participants to complete **3 free investigation labs** on LetsDefend, BTLO, or CyberDefenders, and write **a short write-up for each: alert, evidence, and verdict**.

Each report in this repository has those three sections and points to saved evidence. The badge screenshots show challenge completion, not real-world incident impact.

## Skills demonstrated

- Email header and return-path inspection
- Careful parsing of URLs and domain/brand mismatches
- Wireshark display filters and review of TCP SYN scanning patterns
- Basic NetBIOS and HTTP access-log review
- Evidence-based reporting with explicit confidence limits

## Repository layout

```text
nexlevr-beginner-task-01/
├── README.md
├── 01-phishing-email/
│   ├── README.md
│   └── evidence/
├── 02-port-scan-activity/
│   ├── README.md
│   └── evidence/
├── 03-investigate-web-attack/
│   ├── README.md
│   └── evidence/
├── SUBMISSION.md
└── .gitignore
```

## Scope and integrity

All activities were conducted in **LetsDefend's authorized training environment**. The repository contains screenshots of the provided challenges, not real customer SOC records. It does not contain the lab's raw email archive or complete PCAP/access logs, and it does not claim effects that the retained evidence cannot establish.

**Next:** Publish to GitHub, review the write-ups, showcase the project, and submit the repository link/tag to NEXLEVR for verification. See [SUBMISSION.md](SUBMISSION.md).