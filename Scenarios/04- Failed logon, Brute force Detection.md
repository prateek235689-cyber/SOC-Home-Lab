# Scenario 04 — Repeated Failed Logon / Brute-Force Detection

## 🎯 Objective:
The objective of this scenario is to simulate repeated failed authentication attempts against a Windows endpoint and detect the activity using Windows Security logs and Splunk.
This scenario demonstrates how a SOC analyst can identify abnormal authentication behavior, analyze failed logon events, and develop threshold-based detection logic for potential brute-force activity.

**Failed Authentication Attempts → Windows Event ID 4625 → Splunk → Detection → Investigation**

## 🧪 Lab Environment

** Component : Purpose **  
Kali Linux : Attack simulation system.
Windows : Target endpoint.
Windows Security Logs : Authentication telemetry.
Splunk Enterprise: SIEM and log analysis.
Sysmon : Additional endpoint telemetry.

---

## ⚔️ Attack Simulation:

Multiple controlled failed authentication attempts will be generated against the Windows lab endpoint.
The purpose is to create authentication telemetry resembling repeated password-guessing behavior.
This simulation is performed only against systems in my controlled SOC home lab.

### Attack Evidence
![Failed Logon Simulation](../screenshots/scenario-04-failed-logon/01-failed-logon-simulation.png)

---

## 🔍 Windows Security Log Investigation:
Windows Security logs will be investigated for:

**Event ID 4625 — An account failed to log on**

Relevant fields will include:
- Account Name
- Logon Type
- Failure Reason
- Source Network Address
- Workstation information
- Timestamp

### Windows Event Evidence
![Windows Event 4625](../screenshots/scenario-04-failed-logon/02-windows-event-4625.png)

## 📊 Splunk Investigation:
Windows Security events will be forwarded to Splunk for centralized analysis.
The investigation will search for repeated Event ID 4625 events and determine whether multiple authentication failures occurred within a short period.

### Splunk Evidence
![Splunk Investigation](../screenshots/scenario-04-failed-logon/03-splunk-investigation.png)


## 🚨 Detection Logic
Instead of treating every failed login as malicious, the detection will identify multiple failed authentication attempts occurring within a defined time window.
This threshold-based approach helps distinguish isolated user mistakes from potentially suspicious authentication activity.

### Detection Evidence
![Failed Logon Detection](../screenshots/scenario-04-failed-logon/04-failed-logon-detection.png)


## 🕵️ Analyst Investigation:

The investigation will attempt to determine:
- Which account was targeted?
- How many authentication failures occurred?
- What system generated the attempts?
- What logon type was involved?
- What was the failure reason?
- Did the activity exceed the detection threshold?
- Was there a successful authentication after the failures?


## ⚠️ False Positive Considerations
Multiple failed logins do not automatically indicate an attack.

Possible legitimate causes include:
- Users entering an incorrect password
- Expired or recently changed credentials
- Applications using outdated stored credentials
- Misconfigured services or scheduled tasks


## ✅ Conclusion

This scenario demonstrates the process of collecting Windows authentication telemetry, analyzing failed logon activity in Splunk, and developing threshold-based detection logic for potentially suspicious authentication behavior.

Final findings will be documented after completing and validating the simulation.
