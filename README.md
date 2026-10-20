# SOC Investigation Labs | NEXLEVR Beginner Task 01

NEXLEVR Beginner Level proof of work for all three tasks: LetsDefend investigations, SSH brute-force log analysis, and MITRE ATT&CK mappings.

> **Status:** All three Beginner task reports are published. NEXLEVR submission verification and any certificate are still pending.

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

## Task 02 — Linux SSH Brute-Force Log Analysis

[View the completed Task 02 report and findings table](task-02-brute-force-log-analysis/README.md). Using TryHackMe's Splunk training dataset (`task5`, `linux_secure`), we identified six failed password attempts against `jack-brown` from `10.14.94.82`, followed by one accepted login for that account. Authorization or compromise cannot be confirmed from these records alone.

## Task 03 — MITRE ATT&CK Mapping

[View Task 03 — Five Attack Techniques and Detection Logs](task-03-mitre-attack-mapping/README.md). Covers phishing, brute force, ransomware, credential dumping, and cloud-storage exfiltration with linked ATT&CK technique and detection references.

## Scope

All investigations took place in LetsDefend's training environment. The repository shares write-ups, not real customer information or raw challenge materials. Challenge completion badges are distinct from professional certifications.

See [SUBMISSION.md](SUBMISSION.md) for the review and submission steps.
