# Windows Amcache Analysis

## 📌 Overview
The Amcache.hve registry file is a valuable forensic artifact that tracks executed programs, file metadata, and other system activity. It is essential for identifying program execution and file interactions, even if the program has been deleted.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for Amcache Analysis](#-tools-for-amcache-analysis)
- [Key Amcache Locations and Artifacts](#-key-amcache-locations-and-artifacts)
- [Things to Notice in Amcache Analysis](#-things-to-notice-in-amcache-analysis)
- [Limitations of Amcache Analysis](#-limitations-of-amcache-analysis)
- [Windows Amcache Forensic Cheat Sheet](#-windows-amcache-forensic-cheat-sheet)
- [Sample Log Analysis Files](#-sample-log-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for Amcache Analysis
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **AmcacheParser (Eric Zimmerman)** | Extracts and parses Amcache data | `AmcacheParser.exe -f Amcache.hve -o output.csv` |
| **RECmd (Eric Zimmerman)** | Advanced registry analysis tool | `RECmd.exe -d Amcache.hve` |
| **KAPE (Kroll Artifact Parser and Extractor)** | Extracts and parses Amcache logs | `kape.exe --target Amcache` |
| **Volatility (Memory Analysis)** | Extracts Amcache from memory dumps | `vol.py -f <memory_dump> printkey -K Amcache` |
</details>

---

## 🔍 Key Amcache Locations and Artifacts
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Registry Path** | **What It Reveals** |
|-------------|------------------|----------------------|
| **Program Execution History** | `C:\Windows\AppCompat\Programs\Amcache.hve` | Tracks executed programs |
| **File Metadata** | `Root\File` | Contains details like SHA1 hash, size, and timestamps |
| **Device Information** | `Root\DriverDatabase` | Tracks installed drivers |
| **Persistence Evidence** | `Root\Programs` | Programs set to auto-run on startup |
</details>

---

## ⚠️ Things to Notice in Amcache Analysis
- **Executed Applications:** Identifies software that ran on the system, even if it was deleted.
- **File Hashes and Metadata:** Can be used to compare against threat intelligence databases.
- **Program Install Timestamps:** Useful for forensic timelines and event correlation.
- **Unsigned or Suspicious Programs:** Detect malware or unauthorized applications.
- **Removable Device Executions:** Indicates if a program was executed from a USB drive.

---

## 🚧 Limitations of Amcache Analysis
- **No Full Execution Logs:** Amcache only tracks metadata, not actual command execution.
- **No Direct User Attribution:** Cannot determine which user executed a program.
- **Log Overwriting:** Older entries may be purged as new programs execute.
- **Tampering and Clearing:** Attackers may delete or modify Amcache entries.

---

## 📜 Windows Amcache Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Key Data** | **Registry Path** | **Analysis Notes** |
|-------------|------------------|----------------------|
| **Program Execution** | `Root\File` | Tracks executed applications with timestamps |
| **SHA1 Hash** | `Root\File\SHA1` | Can be compared with known malware signatures |
| **Install Timestamp** | `Root\Programs` | Date/time when an application was installed |
| **Device Information** | `Root\DriverDatabase` | Lists installed and loaded drivers |
</details>

---

## 📂 Sample Log Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample Amcache Data](./samples/sample_amcache_data.reg)
- [Amcache Execution Analysis](./samples/amcache_execution_report.csv)
</details>

---

## 📖 Additional Resources
- [Eric Zimmerman's AmcacheParser](https://ericzimmerman.github.io/)
- [SANS DFIR: Amcache Forensics](https://digital-forensics.sans.org/)
- [Microsoft Docs: Amcache Registry Data](https://learn.microsoft.com/en-us/windows/win32/sysinfo/registry)

---

### ✅ Summary
Windows Amcache analysis is a powerful forensic technique for identifying program execution history, file metadata, and system persistence mechanisms. By leveraging tools like AmcacheParser, RECmd, and Volatility, investigators can extract and analyze critical execution artifacts. However, limitations such as data overwriting, lack of user attribution, and possible tampering must be considered.

