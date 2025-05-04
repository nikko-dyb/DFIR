# Windows Shimcache Analysis

## 📌 Overview
Shimcache (also known as the Application Compatibility Cache) is a forensic artifact stored in the Windows Registry that tracks executed programs, their file paths, and timestamps. This data is useful for reconstructing a timeline of program execution and identifying suspicious or malicious activity.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for Shimcache Analysis](#-tools-for-shimcache-analysis)
- [Key Shimcache Artifacts and Locations](#-key-shimcache-artifacts-and-locations)
- [Things to Notice in Shimcache Analysis](#-things-to-notice-in-shimcache-analysis)
- [Limitations of Shimcache Analysis](#-limitations-of-shimcache-analysis)
- [Windows Shimcache Forensic Cheat Sheet](#-windows-shimcache-forensic-cheat-sheet)
- [Sample Shimcache Analysis Files](#-sample-shimcache-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for Shimcache Analysis
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **ShimCacheParser (Eric Zimmerman)** | Extracts and parses Shimcache data | `ShimCacheParser.exe -f SYSTEM -o output.csv` |
| **RegRipper** | Extracts Shimcache data from registry hives | `rip.pl -r SYSTEM -p shimcache` |
| **RECmd (Eric Zimmerman)** | Advanced registry analysis tool | `RECmd.exe -d SYSTEM` |
| **Volatility (Memory Analysis)** | Extracts Shimcache from memory dumps | `vol.py -f <memory_dump> printkey -K Shimcache` |
</details>

---

## 🔍 Key Shimcache Artifacts and Locations
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Registry Path** | **What It Reveals** |
|-------------|------------------|----------------------|
| **Shimcache Execution Records** | `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache` | Tracks executed applications and timestamps |
| **File Paths of Executed Programs** | Inside Shimcache data | Lists file locations of executed programs |
| **Last Modified Timestamps** | Inside Shimcache metadata | Indicates when the program was last modified |
| **Presence of Malware** | Inside Shimcache | Can indicate if malware was executed |
</details>

---

## ⚠️ Things to Notice in Shimcache Analysis
- **Presence of Malware Executions:** Shimcache records can reveal if a suspicious program was executed.
- **Time Discrepancies:** Last modified timestamps may not match execution timestamps.
- **Evidence of Deleted Programs:** If a program is listed in Shimcache but does not exist on disk, it was likely deleted.
- **Correlate with Other Artifacts:** Cross-reference Shimcache data with Prefetch, Amcache, and Event Logs for a complete picture.
- **No Execution Count:** Unlike Prefetch, Shimcache does not store the number of times a program was executed.

---

## 🚧 Limitations of Shimcache Analysis
- **No Exact Execution Timestamps:** Shimcache records only the last modified date, not execution time.
- **Limited Historical Data:** Older entries may be overwritten as new programs execute.
- **No User Attribution:** Cannot determine which user executed the program.
- **Log Tampering:** Attackers may clear or manipulate Shimcache records.

---

## 📜 Windows Shimcache Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Key Data** | **Registry Path** | **Analysis Notes** |
|-------------|------------------|----------------------|
| **Executed Programs** | `SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache` | Tracks executed applications |
| **File Paths** | Inside Shimcache data | Shows file location of executed applications |
| **Last Modified Timestamp** | Inside Shimcache metadata | Indicates when the application was modified |
| **Malware Indicators** | Inside Shimcache records | Can indicate malicious executions |
</details>

---

## 📂 Sample Shimcache Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample Shimcache Data](./samples/sample_shimcache_data.reg)
- [Shimcache Execution Analysis](./samples/shimcache_execution_report.csv)
</details>

---

## 📖 Additional Resources
- [Eric Zimmerman's ShimCacheParser](https://ericzimmerman.github.io/)
- [SANS DFIR: Shimcache Forensics](https://digital-forensics.sans.org/)
- [Microsoft Docs: Application Compatibility](https://learn.microsoft.com/en-us/windows/deployment/planning/compatibility)

---

### ✅ Summary
Windows Shimcache analysis is a crucial forensic method for tracking program execution history and identifying deleted or malicious programs. By using tools like ShimCacheParser, RegRipper, and Volatility, investigators can extract and analyze execution artifacts. However, analysts must be aware of limitations, including lack of exact execution timestamps and potential log tampering by attackers.

