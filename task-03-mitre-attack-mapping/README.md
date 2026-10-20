# Beginner Task 03 — MITRE ATT&CK Mapping

**Program:** NEXLEVR Cybersecurity Internship — Beginner Level  
**Scope:** Map phishing, brute force, ransomware, credential dumping, and data exfiltration to MITRE ATT&CK techniques and identify the logs that could show each.  
**Research source:** MITRE ATT&CK Enterprise, reviewed October 20, 2026.

## Findings table

| Attack | Representative ATT&CK technique | Tactic | Example log sources |
| --- | --- | --- | --- |
| Phishing (link-based) | [T1566.002 — Spearphishing Link](https://attack.mitre.org/techniques/T1566/002/) | Initial Access | Microsoft 365 message/audit telemetry; Windows Security process creation **4688**; Sysmon network **3** and DNS **22** |
| Brute force (SSH) | [T1110.001 — Password Guessing](https://attack.mitre.org/techniques/T1110/001/) | Credential Access | Linux `auth.log` / `secure` / syslog: `sshd Failed password` and `Accepted password`; Windows Security failed logon **4625** for Windows authentication |
| Ransomware | [T1486 — Data Encrypted for Impact](https://attack.mitre.org/techniques/T1486/) | Impact | Sysmon process creation **1**, file creation **11**; file-integrity monitoring/file-write telemetry, EDR mass-file-change detections |
| Credential dumping | [T1003.001 — LSASS Memory](https://attack.mitre.org/techniques/T1003/001/) | Credential Access | Sysmon process access **10**, process creation **1**, file creation **11**; Windows Security privileged service **4673**; Sysmon registry **13/14** |
| Data exfiltration (cloud uploads) | [T1567.002 — Exfiltration to Cloud Storage](https://attack.mitre.org/techniques/T1567/002/) | Exfiltration | Windows Security file access **4663/4656** and permissions **4670**; Sysmon network **3**, DNS **22**, process creation **1**; proxy and cloud audit logs |

These are *representative* techniques for each attack type, not the only possible technique mappings. The email reviewed in Task 01 was link-based phishing, but available evidence did **not** independently establish targeted spearphishing.

## Detection strategies and investigation notes

### 1. Phishing
- ATT&CK: **T1566.002**, Initial Access.
- [DET0107 — Detection Strategy for Spearphishing Links](https://attack.mitre.org/detectionstrategies/DET0107/), analytic **AN0298**.
- MITRE example telemetry: `m365:unified` for messages with embedded links, Security **4688** for process creation, Sysmon **3/22** for network and DNS activity.
- **SOC correlation:** Follow inbound message → user click evidence (when available) → browser/network requests → unusual child processes. Receiving an email alone does not prove an infection.

### 2. Brute Force
- ATT&CK: **T1110.001**, Credential Access.
- [DET0551 — Password Guessing via Multi-Source Authentication Failure Correlation](https://attack.mitre.org/detectionstrategies/DET0551/), Linux analytic **AN1522**.
- Data component: **DC0002 User Account Authentication**; Linux syslog `sshd[pid]: Failed password`.
- **SOC correlation:** Count failures by source IP and user, account for repeated syslog messages, then check subsequent accepted logins and authorization context.
- **Hands-on connection:** [Beginner Task 02 Linux SSH analysis](../task-02-brute-force-log-analysis/README.md) found **6 failed attempts** for `jack-brown` from `10.14.94.82`, followed by **1 accepted login**. This is suspicious, not proof of compromise.

### 3. Ransomware
- ATT&CK: **T1486**, Impact (Availability).
- [DET0215 — Detection of Multi-Platform File Encryption for Impact](https://attack.mitre.org/detectionstrategies/DET0215/), Windows analytic **AN0602**.
- MITRE table names Sysmon **1**, **11**, and **2**. **Precision note:** Sysmon **2** is specifically *file creation time changed*, not comprehensive file-content modification telemetry; monitor file writes/renames via EDR or file-integrity tooling when possible.
- **SOC correlation:** Unusually frequent file modifications/renames, odd extensions, ransom notes, shadow-copy deletion, and suspicious process execution. A single file write alone is not proof of ransomware.

### 4. Credential Dumping
- ATT&CK: **T1003.001**, Credential Access.
- [DET0363 — Detection of Credential Dumping from LSASS Memory via Access and Dump Sequence](https://attack.mitre.org/detectionstrategies/DET0363/), analytic **AN1030**.
- Sysmon **10** for process access (e.g. access to `lsass.exe`), Sysmon **1** for process creation, Sysmon **11** for new dump files, Security **4673** for privileged service use, and Sysmon **13/14** for registry activity.
- **SOC correlation:** Examine process lineage, requested access rights, unusual memory dump file creation, and whether the access came from legitimate AV/EDR/diagnostic software.

### 5. Data Exfiltration
- ATT&CK: **T1567.002**, Exfiltration.
- [DET0570 — Detection Strategy for Exfiltration to Cloud Storage](https://attack.mitre.org/detectionstrategies/DET0570/), Windows analytic **AN1571**.
- MITRE table: Windows Security **4663, 4670, 4656**; Sysmon **3, 22** and **1**.
- **SOC correlation:** Sensitive file access followed by unusually large outbound HTTPS connections and DNS activity associated with cloud storage. Proxy/NetFlow, cloud audit and DLP logs help determine volume, content and authorization. DNS and connection logs alone do not prove uploads.

## Evidence handling

Official MITRE pages were inspected during the exercise, and screenshots were retained locally in the chat. **Screenshots have not been uploaded to this GitHub folder.** NEXLEVR requested the mapping and relevant logs, not a fixed screenshot count.

## Conclusion

The five mappings show how ATT&CK IDs, tactics, detection strategies, analytics, and specific event sources fit together. Practical detection requires correlation across logs and context: a single event usually cannot prove intent, maliciousness, or impact.
