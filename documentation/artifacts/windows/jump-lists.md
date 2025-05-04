# Windows Jump List Analysis

## 📌 Overview
Jump Lists are forensic artifacts in Windows that track recently and frequently accessed files and applications. These artifacts can provide valuable insights into user activity, even if files have been deleted.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for Jump List Analysis](#-tools-for-jump-list-analysis)
- [Key Jump List Locations and Artifacts](#-key-jump-list-locations-and-artifacts)
- [Things to Notice in Jump List Analysis](#-things-to-notice-in-jump-list-analysis)
- [Limitations of Jump List Analysis](#-limitations-of-jump-list-analysis)
- [Windows Jump List Forensic Cheat Sheet](#-windows-jump-list-forensic-cheat-sheet)
- [Sample Log Analysis Files](#-sample-log-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for Jump List Analysis
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **JLECmd (Eric Zimmerman)** | Extracts and parses Jump Lists | `JLECmd.exe -d <directory>` |
| **JumpListExplorer** | GUI tool for analyzing Jump List artifacts | Interactive analysis |
| **RECmd (Eric Zimmerman)** | Advanced registry analysis tool | `RECmd.exe -d <hive>` |
| **ForensicsArtifacts.com Tools** | Collection of Jump List parsers | Various CLI tools |
</details>

---

## 🔍 Key Jump List Locations and Artifacts
<details>
  <summary>Click to expand</summary>

| **Artifact** | **File Path** | **What It Reveals** |
|-------------|-------------|----------------------|
| **Automatic Jump Lists** | `%APPDATA%\Microsoft\Windows\Recent\AutomaticDestinations` | Tracks automatically generated recent files |
| **Custom Jump Lists** | `%APPDATA%\Microsoft\Windows\Recent\CustomDestinations` | Tracks user-pinned files |
| **LNK File Links** | `%APPDATA%\Roaming\Microsoft\Windows\Recent` | Shortcut links to accessed files |
</details>

---

## ⚠️ Things to Notice in Jump List Analysis
- **User File Access Patterns:** Can identify user access to files even if they were deleted.
- **Application Usage:** Shows frequently used programs and their linked files.
- **Correlate with Other Artifacts:** Combine Jump List data with Prefetch, Registry, and Shellbags for a complete timeline.
- **Timestamps:** Useful for reconstructing user activity timelines.

---

## 🚧 Limitations of Jump List Analysis
- **No Direct File Contents:** Jump Lists track file paths, not file content.
- **May Be Cleared by the User:** Users can manually clear Jump Lists from Windows.
- **Does Not Track External Devices:** USB or network drive files may not always be logged.

---

## 📜 Windows Jump List Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Artifact** | **File Path** | **Analysis Notes** |
|-------------|-------------|----------------------|
| **Recent Files** | `%APPDATA%\Microsoft\Windows\Recent` | Tracks recent file usage |
| **Jump List AutoDestinations** | `%APPDATA%\Microsoft\Windows\Recent\AutomaticDestinations` | Contains MRU (Most Recently Used) file paths |
| **Jump List CustomDestinations** | `%APPDATA%\Microsoft\Windows\Recent\CustomDestinations` | User-defined pinned files |
</details>

---

## 📂 Sample Log Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample Jump List Data](./samples/sample_jumplist_data.bin)
- [Jump List Log Analysis](./samples/jumplist_analysis_report.csv)
</details>

---

## 📖 Additional Resources
- [Eric Zimmerman's JLECmd](https://ericzimmerman.github.io/)
- [SANS DFIR: Windows Jump Lists](https://digital-forensics.sans.org/)
- [Microsoft Docs: Windows Shell Data](https://learn.microsoft.com/en-us/windows/win32/shell/shell-registry-entries)

---

### ✅ Summary
Jump List analysis provides forensic investigators with key insights into recent file and application usage. By leveraging tools like JLECmd and JumpListExplorer, forensic analysts can reconstruct a user’s activity timeline. However, limitations such as manual deletion and lack of file content tracking should be considered.

