# Task 01 — Screenshot evidence

Screenshots were captured from the user's **NEXLEVR-Wazuh** personal lab on October 22, 2026.

## Evidence files to upload

1. `01-virtualbox-nexlevr-vm.png` — separate VM / NAT forwarding
2. `02-ubuntu-server.png` — Ubuntu Server version and hostname
3. `03-wazuh-services.png` — four services shown as active
4. `04-wazuh-dashboard.png` — successful dashboard access
5. `05-test-activity.png` — sanitized local SSH authentication failures
6. `06-wazuh-alerts.png` — six matching Wazuh detections
7. `07-alert-investigation.png` — Wazuh rule 2502 detail with T1110 mapping

**Upload status:** Images are not included in this initial GitHub documentation commit. Do not mark them uploaded until the actual PNGs are committed.

## Before publishing screenshots

- Exclude all terminal output containing `wazuh-passwords.txt`, admin passwords, service-account credentials or tokens.
- If an image also contains an exposed password elsewhere on the desktop, crop/redact that area before using it.
- Do not include confidential real-client tenant names, case numbers or production logs.
- Prefer full, readable alert details, including timestamp, rule ID, rule level and description.

Return to the [Task 01 report](../README.md).
