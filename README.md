# SOC Investigation Labs | NEXLEVR Beginner Task 01

Three LetsDefend training investigations, documented for **NEXLEVR Beginner Level — Task 01**.

> **Status:** All 3 investigation labs completed and all 3 short write-ups published. This is **Task 01 of 3** in the Beginner category. Tasks 02 (authentication log analysis) and 03 (MITRE ATT&CK mapping) are still to be completed. NEXLEVR has not verified the submission or issued a certificate.

## Investigations

| Lab | Tools | Brief verdict | Completion |
| --- | --- | --- | --- |
| [01 — Phishing Email](01-phishing-email/README.md) | Thunderbird, email headers, URL inspection | Likely phishing; no demonstrated compromise | Oct 19, 2026 — Phishing Analyzer |
| [02 — Port Scan Activity](02-port-scan-activity/README.md) | Wireshark, PCAP, SYN and NBNS filters | Scanning behavior; no proven intrusion | Oct 19, 2026 — Detector |
| [03 — Investigate Web Attack](03-investigate-web-attack/README.md) | Linux, HTTP access.log review | Challenge completed; exploit outcome not independently established from saved extracts | Oct 20, 2026 — Web Attack Investigated |

## Official Task 01 requirement

Complete **three free investigation labs** on LetsDefend, BTLO, or CyberDefenders and write a **short write-up for each** explaining **the alert, the evidence, and your verdict**.

**There is no stated requirement to upload ten screenshots, or any fixed number of screenshots.** Optional evidence screenshots may be added if helpful for demonstrating findings. The three short reports are the core deliverables.

## Methods and skills

- Email header and Return-Path inspection; checking embedded link domains
- TCP SYN packet analysis and source/target identification in Wireshark
- Reading web server access logs and distinguishing ordinary requests from suspicious patterns
- Clear verdicts that do not overstate what the available evidence proves

## Beginner category remaining work

- **Task 02:** Analyze sample Windows Event Logs or Linux auth logs for brute-force login patterns; present findings in a table
- **Task 03:** Map phishing, brute force, ransomware, credential dumping, and data exfiltration to MITRE ATT&CK techniques and identify relevant logs

## Scope

All investigations took place in LetsDefend's training environment. The repository shares write-ups, not real customer information or raw challenge materials. Challenge completion badges are distinct from professional certifications.

See [SUBMISSION.md](SUBMISSION.md) for the review and submission steps.
