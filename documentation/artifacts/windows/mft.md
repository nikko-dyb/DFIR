# Windows Master File Table (MFT) Analysis

## 📌 Overview
The Master File Table (MFT) is a fundamental component of the NTFS file system, storing metadata about all files and directories on a volume. It is a crucial artifact for forensic investigations, providing details on file creation, modification, access, and deletion.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for MFT Analysis](#-tools-for-mft-analysis)
- [Key MFT Locations and Artifacts](#-key-mft-locations-and-artifacts)
- [Things to Notice in MFT Analysis](#-things-to-notice-in-mft-analysis)
- [Limitations of MFT Analysis](#-limitations-of-mft-analysis)
- [Windows MFT Forensic Cheat Sheet](#-windows-mft-forensic-cheat-sheet)
- [Sample Log Analysis Files](#-sample-log-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for MFT Analysis
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **MFTECmd (Eric Zimmerman)** | Parses and extracts MFT data | `MFTECmd.exe -f $MFT -o output.csv` |
| **AnalyzeMFT.py** | Python script for parsing MFT entries | `analyzeMFT.py -f $MFT -o output.csv` |
| **FTK Imager** | Extracts and views MFT structures | GUI-based analysis |
| **Autopsy** | Open-source digital forensics tool | GUI-based MFT analysis |
| **X-Ways Forensics** | Advanced forensic suite | Interactive file system analysis |
</details>

---

## 🔍 Key MFT Locations and Artifacts
<details>
  <summary>Click to expand</summary>

| **Artifact** | **File Path** | **What It Reveals** |
|-------------|-------------|----------------------|
| **Master File Table (MFT)** | `C:\$MFT` | Contains metadata of all files on NTFS volume |
| **File Record Numbers** | Inside MFT entries | Unique identifiers for each file |
| **Timestamps (MACB)** | Inside MFT entries | Tracks file creation, modification, access, and metadata changes |
| **Resident vs Non-Resident Files** | MFT entry structure | Determines if data is stored in MFT or externally |
| **Deleted File Entries** | Available until overwritten | Identifies deleted files and forensic recoverability |
</details>

---

## ⚠️ Things to Notice in MFT Analysis
- **File System Timeline Reconstruction:** Use timestamps to correlate file activity with an event timeline.
- **Deleted or Overwritten Files:** MFT keeps records of deleted files until overwritten by new data.
- **Timestamps (MACB):** Monitor Metadata Modified (M), Accessed (A), Created (C), and Entry Modified (B) values.
- **Evidence of Anti-Forensic Activities:** Look for file timestamp manipulation or wiping tools.
- **Resident vs. Non-Resident Data:** Large files are typically stored outside the MFT, while small files may reside within it.

---

## 🚧 Limitations of MFT Analysis
- **File Content Not Stored in MFT:** The MFT contains metadata but not actual file contents.
- **Possible Overwriting:** Deleted file records may be lost if new data overwrites them.
- **Timestamps Can Be Manipulated:** Attackers may alter MACB timestamps using anti-forensic tools.
- **Limited Visibility on FAT or exFAT:** The MFT is exclusive to NTFS, making other file systems less forensic-friendly.

---

## 📜 Windows MFT Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Key Data** | **Description** | **Analysis Notes** |
|-------------|------------------|----------------------|
| **File Reference Number** | Unique ID for each file | Helps track file movements |
| **Parent File Reference** | ID of parent directory | Useful for directory reconstruction |
| **MACB Timestamps** | Modification, Access, Created, Entry Modified | Helps build forensic timelines |
| **File Size and Attributes** | Stored in MFT entries | Identifies file properties |
| **Deleted File Entries** | Available until overwritten | Can indicate attempted data destruction |
</details>

---

## 📂 Sample Log Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample MFT Extract](./samples/sample_mft_extract.csv)
- [MFT Timeline Analysis](./samples/mft_timeline_report.csv)
</details>

---

## 📖 Additional Resources
- [Eric Zimmerman's MFTECmd](https://ericzimmerman.github.io/)
- [SANS DFIR: MFT Analysis](https://digital-forensics.sans.org/)
- [Microsoft Docs: NTFS File System](https://learn.microsoft.com/en-us/windows/win32/fileio/ntfs-file-system)

---

### ✅ Summary
Master File Table (MFT) analysis is essential in digital forensics for tracking file activity, metadata changes, and deleted file recovery. By leveraging tools like MFTECmd, AnalyzeMFT.py, and FTK Imager, forensic investigators can extract and analyze critical file system metadata. However, analysts should be aware of potential limitations, such as overwriting of deleted records and timestamp manipulation.