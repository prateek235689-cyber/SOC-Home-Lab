# Scenario 01 — Network Reconnaissance Simulation!

**Objective:**
Simulate network reconnaissance against the Windows endpoint from a
Kali Linux attacker machine and investigate the resulting telemetry
using Sysmon and Splunk.

**Lab Environment:**
- Attacker: Kali Linux
- Target: Windows
- Endpoint Telemetry: Sysmon
- SIEM: Splunk Enterprise
- Sysmon Event ID investigated: Event ID 3 — Network Connection

**Attack Simulation**
A TCP Connect scan was performed from the Kali Linux machine against
the Windows lab endpoint.

**kali linux command:**
nmap -sT <WINDOWS-LAB-IP>

The purpose of the scan was to identify accessible TCP ports and services on the target endpoint.

### Attack Evidence

![Nmap TCP Connect Scan](../screenshots/scenario-01-network-reconnaissance/01-nmap-scan.png)

---

## 🔍 Sysmon Investigation
Sysmon was used to investigate network connection telemetry generated on the Windows endpoint.
The primary event investigated in this scenario was:

**Sysmon Event ID 3 — Network Connection**

### Sysmon Evidence
![Sysmon Event ID 3](../screenshots/scenario-01-network-reconnaissance/02-sysmon-event.png)

## 📊 Splunk Investigation
Sysmon telemetry was ingested into Splunk Enterprise for centralized analysis.

The initial SPL query used to investigate network connection events was:

```spl
index=main sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventID=3
```

### Splunk Telemetry
![Splunk Sysmon Telemetry](../screenshots/scenario-01-network-reconnaissance/03-splunk-telemetry.png)

---

## 🚨 Detection Logic
The detection query will be developed after analyzing the network telemetry generated during the reconnaissance activity.
<!-- Final SPL detection query will be added here -->

### Detection Evidence
![Splunk Detection](../screenshots/scenario-01-network-reconnaissance/04-splunk-detection.png)
