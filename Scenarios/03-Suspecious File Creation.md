# Scenario 03 — Suspicious File Creation Detection

## 🎯 Objective:
The objective of this scenario is to simulate the creation of a suspicious PowerShell script inside the Windows temporary directory and detect the activity using Sysmon and Splunk.
This scenario demonstrates how a SOC analyst can investigate suspicious file creation activity using endpoint telemetry.

**File Creation:
→ Sysmon Event ID 11 → Splunk → Detection → Investigation**

## 🧪 Attack Simulation

A PowerShell script file was deliberately created inside the Windows `%TEMP%` directory to simulate suspicious file-drop behavior.

```powershell
New-Item -Path "$env:TEMP\suspicious_payload.ps1" -ItemType File -Force
```

Harmless test content was then written to the file:

```powershell
Set-Content -Path "$env:TEMP\suspicious_payload.ps1" -Value 'Write-Host "SOC Home Lab Test"'
```

> This was a benign simulation performed only inside my controlled SOC home lab. No malicious payload was executed.

### Attack Evidence
![Suspicious File Creation](../screenshots/scenario-03-file-creation/01-file-creation.png)


## 🔍 Sysmon Investigation
Sysmon telemetry was analyzed to identify the creation of the suspicious `.ps1` file.

**Sysmon Event ID 11 — File Create** was used for this investigation.

Important information investigated included:
- Process responsible for creating the file
- Target filename
- File creation timestamp
- User associated with the activity

### Sysmon Evidence
![Sysmon Event ID 11](../screenshots/scenario-03-file-creation/02-sysmon-event-11.png)


## 📊 Splunk Investigation
Sysmon logs were ingested into Splunk Enterprise and searched for the suspicious file.

```spl
index=main sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" EventID=11
"suspicious_payload.ps1"
```

### Splunk Evidence
![Splunk Investigation](../screenshots/scenario-03-file-creation/03-splunk-investigation.png)


## 🚨 Detection Logic
The detection focuses on PowerShell script files being created in temporary directories.
The final SPL detection query will be added after validating the generated telemetry.

### Detection Evidence
![File Creation Detection](../screenshots/scenario-03-file-creation/04-file-creation-detection.png)


## 🕵️ Analyst Findings
The investigation will determine:

- Which process created the file
- Where the file was created
- Which user was responsible
- Whether the file type and location are unusual
- Whether additional suspicious activity occurred around the same timestamp


## 🛡️ MITRE ATT&CK Mapping
MITRE ATT&CK mapping will be added only after validating which technique accurately represents the observed behavior.

## ✅ Conclusion
This scenario demonstrates how Sysmon file-creation telemetry can be centralized and investigated using Splunk. The exercise provides hands-on experience with endpoint monitoring, SPL searching, and SOC-style analysis of potentially suspicious file activity.
