# Lab 02 — Port Scan Activity

**Platform:** LetsDefend | **Completed:** October 19, 2026 | **Badge:** Detector

## Alert / Scenario
The challenge provided a `port_scan.pcap` network capture to determine whether port-scanning behavior occurred and identify systems in the traffic.

## Evidence
In Wireshark, used the display filter:

```wireshark
tcp.flags.syn == 1 && tcp.flags.ack == 0
```

- Repeated initial TCP SYN requests from **`10.42.42.253`** targeted multiple hosts and destination ports.
- Examples of destination hosts: **`10.42.42.50`**, **`10.42.42.56`**, **`10.42.42.25`**.
- The screenshot showed **7,428 displayed packets** of **13,625 total** under this filter. The displayed count alone does not determine intent.
- Additional filter: `smb || smb2 || nbns || ntlmssp` showed NBNS traffic from `10.42.42.50` and `10.42.42.25`. The exercise accepted `10.42.42.50` as the Windows system; NBNS alone cannot reliably establish OS.
- A verified Apple device MAC address was not retained in our available evidence, so none is invented here.

## Verdict
**Port scanning observed.** Repeated probes toward different ports and hosts support network reconnaissance. Whether scanning was authorized, or any exploit succeeded, was not established by these excerpts.

**Suggested action:** Correlate source asset ownership and the scan schedule with firewall and endpoint records before escalating.

## Completion
LetsDefend **Detector** badge earned October 19, 2026. The full PCAP is not redistributed.
