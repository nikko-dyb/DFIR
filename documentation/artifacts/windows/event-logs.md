# Windows Event Log Analysis

## 📌 Overview
Windows Event Logs (EVTX) provide a detailed record of system, security, and application activity. These logs are crucial for forensic investigations, helping analysts detect unauthorized access, malware activity, and system modifications.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for Event Log Analysis](#-tools-for-event-log-analysis)
- [Key Event Log Locations and Artifacts](#-key-event-log-locations-and-artifacts)
- [Things to Notice in Event Log Analysis](#-things-to-notice-in-event-log-analysis)
- [Limitations of Event Log Analysis](#-limitations-of-event-log-analysis)
- [Windows Event Log Forensic Cheat Sheet](#-windows-event-log-forensic-cheat-sheet)
- [Sample Log Analysis Files](#-sample-log-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for Event Log Analysis
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **Event Viewer (Windows)** | Built-in tool to view Windows Event Logs | `eventvwr.msc` |
| **LogParser** | Microsoft tool for querying event logs | `logparser -i:EVT "SELECT * FROM <log.evtx>"` |
| **EVTXECmd (Eric Zimmerman)** | Parses Windows Event Logs | `EVTXECmd.exe -d <directory>` |
| **KAPE (Kroll Artifact Parser and Extractor)** | Extracts and parses event logs | `kape.exe --target EventLogs` |
| **Chainsaw** | Fast event log forensics and detection | `chainsaw hunt <log.evtx>` |
</details>

---

## 🔍 Key Event Log Locations and Artifacts
<details>
  <summary>Click to expand</summary>

| **Log Name** | **File Path** | **What It Reveals** |
|-------------|-------------|----------------------|
| **System Logs** | `C:\Windows\System32\winevt\Logs\System.evtx` | System boot, shutdown, hardware issues |
| **Security Logs** | `C:\Windows\System32\winevt\Logs\Security.evtx` | Logon events, privilege escalation, security breaches |
| **Application Logs** | `C:\Windows\System32\winevt\Logs\Application.evtx` | Application crashes, errors, or warnings |
| **Setup Logs** | `C:\Windows\System32\winevt\Logs\Setup.evtx` | System installations and updates |
| **PowerShell Logs** | `C:\Windows\System32\winevt\Logs\Microsoft-Windows-PowerShell%4Operational.evtx` | PowerShell command execution |
| **Task Scheduler Logs** | `C:\Windows\System32\winevt\Logs\Microsoft-Windows-TaskScheduler%4Operational.evtx` | Scheduled task execution history |
</details>

---

## ⚠️ Things to Notice in Event Log Analysis
- **Logon Events (4624, 4625, 4634, 4648):** Monitor for failed and successful logins.
- **Privilege Escalation (4672, 4690):** Look for administrator-level access attempts.
- **Account Creation/Modification (4720, 4738):** New accounts or changes to user permissions.
- **Service and Process Execution (7045, 4688):** Detect newly installed services and suspicious process execution.
- **PowerShell Activity (4103, 4104):** Check for suspicious PowerShell command execution.

---

## 🚧 Limitations of Event Log Analysis
- **Log Tampering:** Attackers may delete or modify logs to cover their tracks.
- **Retention Period:** Event logs have a size limit and may be overwritten if not archived.
- **False Positives:** Some events may be normal system behavior, requiring correlation with other forensic data.
- **Disabled Logging:** Some critical logs (e.g., Security logs) may be disabled by default or turned off by attackers.

---

## 📜 Windows Event Log Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Event ID** | **Log Source** | **Description** |
|-------------|-------------|----------------------|
| **4624** | Security | Successful logon |
| **4625** | Security | Failed logon attempt |
| **4634** | Security | Logoff event |
| **4672** | Security | Special privileges assigned to new logon |
| **4690** | Security | Attempt to modify service permissions |
| **4720** | Security | User account creation |
| **4688** | System | New process creation |
| **7045** | System | Service installed |
| **4103** | PowerShell | PowerShell script block logging |
| **4104** | PowerShell | Script execution tracking |
</details>

---

## 📂 Sample Log Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample Security Event Log](./samples/sample_security.evtx)
- [PowerShell Event Analysis](./samples/powershell_events_report.csv)
</details>

---

## 📖 Additional Resources
- [Microsoft Docs: Event Logging](https://learn.microsoft.com/en-us/windows/win32/wes/windows-event-log)
- [SANS DFIR: Windows Event Log Forensics](https://digital-forensics.sans.org/)
- [Eric Zimmerman's EVTXECmd](https://ericzimmerman.github.io/)

---

### ✅ Summary
Windows Event Logs are a valuable forensic resource for analyzing system, security, and application events. By leveraging tools like Event Viewer, EVTXECmd, and Chainsaw, investigators can reconstruct user activity and detect potential threats. However, event logs have limitations, including possible tampering, log retention issues, and false positives.