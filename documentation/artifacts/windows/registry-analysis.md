# Windows Registry Analysis

## 📌 Overview
The Windows Registry is a critical forensic artifact that stores system and user settings, application data, and execution history. Investigating the registry can provide insights into user activity, malware persistence, and system modifications.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for Registry Analysis](#-tools-for-registry-analysis)
- [Key Registry Locations and Artifacts](#-key-registry-locations-and-artifacts)
- [Things to Notice in Registry Analysis](#-things-to-notice-in-registry-analysis)
- [Limitations of Registry Analysis](#-limitations-of-registry-analysis)
- [Windows Registry Forensic Cheat Sheet](#-windows-registry-forensic-cheat-sheet)
- [Sample Log Analysis Files](#-sample-log-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for Registry Analysis
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **RegEdit** | Built-in Windows Registry Editor | Manual inspection of registry hives |
| **RegRipper** | Automated registry parsing tool | `rip.pl -r <hive> -p <plugin>` |
| **RECmd (Eric Zimmerman's Tool)** | Advanced registry analysis tool | `RECmd.exe -d <hive>` |
| **Registry Explorer (Eric Zimmerman)** | GUI tool for detailed registry examination | Interactive analysis |
| **Volatility (for memory analysis)** | Extracts registry hives from memory dumps | `vol.py -f <memory_dump> hivelist` |
| **KAPE (Kroll Artifact Parser and Extractor)** | Automates registry extraction & parsing | `kape.exe --target Registry` |
</details>

---

## 🔍 Key Registry Locations and Artifacts
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Registry Path** | **What It Reveals** |
|-------------|------------------|----------------------|
| **User Logins** | `SAM\Domains\Account\Users` | User account details |
| **Last Logged-In User** | `SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI` | Last user to log in |
| **Auto-Run Programs** | `SOFTWARE\Microsoft\Windows\CurrentVersion\Run` | Programs set to run at startup |
| **USB Device History** | `SYSTEM\CurrentControlSet\Enum\USBSTOR` | Connected USB devices |
| **Network Connections** | `SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections` | Proxy & network settings |
| **Recent Files (Open/Save MRU)** | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs` | Recently accessed files |
| **Executed Programs (Amcache & Shimcache)** | `Amcache.hve` & `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache` | Program execution history |
| **User Shellbags (Folder Navigation History)** | `NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU` | Tracks user file/folder navigation |
| **RDP Connection History** | `NTUSER.DAT\Software\Microsoft\Terminal Server Client\Default` | Remote desktop connections |
</details>

---

## ⚠️ Things to Notice in Registry Analysis
- **Timestamps:** Many registry keys store `LastWrite` times, which can help build a forensic timeline.
- **Persistence Mechanisms:** Look for malware persistence in `Run` keys, `Services`, and `Task Scheduler`.
- **Deleted or Modified Keys:** Use forensic tools to recover deleted registry entries.
- **Signs of Intrusion:** Unusual users, unexpected software in `Run` keys, or changes in security settings may indicate compromise.
- **Malware Indicators:** Check for suspicious execution records in `Shimcache` and `Amcache`.
- **Hidden User Accounts:** Suspicious entries in `SAM` and `Security` hives may reveal unauthorized accounts.

---

## 🚧 Limitations of Registry Analysis
- **Registry Changes Frequently:** Many registry keys are modified constantly, making it difficult to attribute specific changes.
- **Limited Historical Data:** The registry does not maintain full historical records, only the latest state.
- **Deleted Entries Are Hard to Recover:** Some deletions leave traces, but many are unrecoverable without memory analysis.
- **Anti-Forensic Techniques:** Malware can obfuscate or delete registry keys to evade detection.

---

## 📜 Windows Registry Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Registry Path** | **Analysis Notes** |
|-------------|------------------|----------------------|
| **UserAssist** | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist` | Tracks user activity |
| **AppCompatCache (ShimCache)** | `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache` | Tracks executed programs |
| **LNK Files** | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs` | Tracks recently accessed files |
</details>

---

## 📂 Sample Log Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample Registry Hive Dump](./samples/sample_registry_hive.reg)
- [Windows Event Log Analysis (EVTX)](./samples/sample_windows_event.evtx)
- [USB Forensic Tracking Report](./samples/usb_forensic_tracking.csv)
</details>

---

## 📖 Additional Resources
- [Microsoft Docs: Windows Registry](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry)
- [SANS DFIR: Windows Registry Forensics](https://digital-forensics.sans.org/)
- [Eric Zimmerman's Registry Tools](https://ericzimmerman.github.io/)

---

### ✅ Summary
Windows registry analysis is a powerful technique in DFIR, providing critical insights into user activity, malware persistence, and system modifications. By leveraging tools like RegRipper, RECmd, and Volatility, forensic investigators can extract and analyze registry data effectively. However, it is important to be aware of the limitations and potential anti-forensic techniques that may hinder analysis.

