# Windows Shellbags Analysis

## 📌 Overview
Windows Shellbags are forensic artifacts that track user navigation within Windows Explorer, storing folder interactions, timestamps, and even deleted directory information. They are a valuable resource for forensic investigators to establish user activity timelines.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for Shellbags Analysis](#-tools-for-shellbags-analysis)
- [Key Shellbags Locations and Artifacts](#-key-shellbags-locations-and-artifacts)
- [Things to Notice in Shellbags Analysis](#-things-to-notice-in-shellbags-analysis)
- [Limitations of Shellbags Analysis](#-limitations-of-shellbags-analysis)
- [Windows Shellbags Forensic Cheat Sheet](#-windows-shellbags-forensic-cheat-sheet)
- [Sample Log Analysis Files](#-sample-log-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for Shellbags Analysis
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **ShellBagsExplorer (Eric Zimmerman)** | GUI tool for parsing Shellbags data | Interactive analysis |
| **SBEcmd (Eric Zimmerman)** | Command-line tool for parsing Shellbags | `SBEcmd.exe -f <hive>` |
| **RegRipper** | Automated registry parsing tool | `rip.pl -r NTUSER.DAT -p shellbags` |
| **RECmd (Eric Zimmerman)** | Advanced registry analysis tool | `RECmd.exe -d NTUSER.DAT` |
| **Volatility (Memory Analysis)** | Extracts Shellbags from memory dumps | `vol.py -f <memory_dump> printkey -K shellbags` |
</details>

---

## 🔍 Key Shellbags Locations and Artifacts
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Registry Path** | **What It Reveals** |
|-------------|------------------|----------------------|
| **User Folder Navigation** | `NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU` | Tracks user file/folder navigation |
| **Folder View Settings** | `NTUSER.DAT\Software\Microsoft\Windows\ShellNoRoam\Bags` | Stores folder display preferences |
| **Deleted Folder Evidence** | `NTUSER.DAT\Software\Microsoft\Windows\Shell` | May contain artifacts from deleted folders |
</details>

---

## ⚠️ Things to Notice in Shellbags Analysis
- **Accessed vs. Deleted Folders:** Shellbags may show records of directories that no longer exist.
- **Timestamps:** Entries provide `LastWrite` timestamps that can help in forensic timelines.
- **Remote Drive and USB Usage:** If users accessed external storage, Shellbags might store evidence.
- **Persistence Evidence:** Malware may manipulate Shellbags to evade detection.

---

## 🚧 Limitations of Shellbags Analysis
- **No File-Level Data:** Shellbags track folders, but not individual files.
- **Limited Historical Retention:** Some data may be overwritten as the registry updates.
- **Encryption and Obfuscation:** Advanced threats may modify or clear Shellbags entries.

---

## 📜 Windows Shellbags Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Registry Path** | **Analysis Notes** |
|-------------|------------------|----------------------|
| **Recent Folders Accessed** | `NTUSER.DAT\Software\Microsoft\Windows\Shell\BagMRU` | Tracks folders a user accessed |
| **Folder Display Preferences** | `NTUSER.DAT\Software\Microsoft\Windows\ShellNoRoam\Bags` | Indicates user customization |
</details>

---

## 📂 Sample Log Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample Shellbags Registry Dump](./samples/sample_shellbags_hive.reg)
- [Shellbags Log Analysis](./samples/shellbags_analysis_report.csv)
</details>

---

## 📖 Additional Resources
- [Eric Zimmerman's ShellBagsExplorer](https://ericzimmerman.github.io/)
- [SANS DFIR: Windows Shellbags Forensics](https://digital-forensics.sans.org/)
- [Microsoft Docs: Registry Shell Data](https://learn.microsoft.com/en-us/windows/win32/shell/shell-registry-entries)

---

### ✅ Summary
Windows Shellbags analysis provides critical forensic insights into user navigation behavior, including deleted folder tracking and external device usage. Leveraging tools like ShellBagsExplorer, RegRipper, and Volatility, forensic investigators can uncover user activity even if files and folders have been deleted. However, Shellbags have limitations, such as lacking file-level tracking and susceptibility to anti-forensic manipulation.

