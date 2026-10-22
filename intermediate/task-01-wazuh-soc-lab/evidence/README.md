# Task 01 — Selected evidence screenshots

Exactly **eight screenshots**, taken from the separate NEXLEVR-Wazuh VirtualBox lab on October 22, 2026, are included in the local submission ZIP.

| Filename | Content |
| --- | --- |
| `01-ubuntu-server-information.png` | Ubuntu Server version and hostname |
| `02-wazuh-services-active.png` | Wazuh service verification: four `active` results |
| `03-virtualbox-port-forwarding.png` | VirtualBox dashboard NAT port forwarding |
| `04-wazuh-login.png` | Wazuh login page (no credentials shown) |
| `05-wazuh-dashboard.png` | Wazuh overview |
| `06-test-activity.png` | Failed SSH login test and journal entries |
| `07-wazuh-alerts.png` | Six matching SSH alerts in Threat Hunting |
| `08-alert-investigation.png` | Rule 2502 details and ATT&CK T1110 mapping |

**Status:** These PNGs have been selected and reviewed. They have **not yet been uploaded to GitHub**. The README deliberately does not display broken image links or claim uploaded images.

## Upload

1. Extract the provided `NEXLEVR_Intermediate_Task01_Selected_Evidence.zip` locally.
2. Open this repository's `intermediate/task-01-wazuh-soc-lab/evidence/` directory.
3. In GitHub, choose **Add file → Upload files** and select the eight PNGs (not this README).
4. Review the commit preview and submit the new files.
5. Check that each image opens in the GitHub directory.

Do not include any older screenshot showing `wazuh-passwords.txt`, the Wazuh password list, filled-in password fields, API credentials, or tokens. The previously exposed lab credentials still need rotation.

[Back to Task 01 report](../README.md).
