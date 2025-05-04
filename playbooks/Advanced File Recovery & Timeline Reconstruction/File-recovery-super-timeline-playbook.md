# Classification: Public

# Advanced File Recovery & Timeline Reconstruction Playbook

## 📌 Preface
This playbook provides a standardized, step-by-step guide for **recovering deleted files** and **reconstructing forensic timelines** using Windows artifacts. It is designed for forensic investigators, SOC analysts, and incident responders to track file deletions, modifications, and system activity efficiently. The workflow aligns with industry best practices and regulatory compliance requirements.

## 📖 Table of Contents
1. Overview
2. Assessment Phase
3. Response Phase
4. Post-Incident Analysis
5. Appendix

---

## 🔍 1. Overview
File recovery and timeline reconstruction are crucial forensic tasks used to recover lost or deleted data and map out historical system activity. These methods support incident response, insider threat investigations, and forensic case-building.

Key objectives:
- **Recover deleted or lost files** using NTFS file system artifacts.
- **Reconstruct a system activity timeline** based on log files and timestamps.
- **Correlate recovered data** with incident events for investigative purposes.

---

## 🔎 2. Assessment Phase
Once an incident involving data loss or unauthorized file deletion is reported, the first step is assessment. Key activities include:

### **Activity 1: Identify Impacted Files**
- Use `$MFT` to check metadata of deleted files:
  ```bash
  MFTECmd.exe -f C:\$MFT -o mft_analysis.csv
  ```
- Scan `$LogFile` for recent file deletions:
  ```bash
  LogFileParser.exe -f C:\$LogFile -o logfile_analysis.csv
  ```

### **Activity 2: Identify Relevant Timeframes**
- Check Event Logs for file modification events:
  ```powershell
  wevtutil qe Security /q:"*[System/EventID=4663]" /rd:true /f:text > file_access_log.txt
  ```
- Analyze Prefetch files for program execution evidence:
  ```bash
  PECmd.exe -d C:\Windows\Prefetch -o prefetch_analysis.csv
  ```

---

## 🚨 3. Response Phase
This phase focuses on recovering deleted files and reconstructing a timeline.

### **Step 1: Recover Deleted Files**
- **Using FTK Imager**:
  1. Open FTK Imager and load the forensic disk image.
  2. Navigate to `$MFT` and extract recoverable files.
- **Using TestDisk**:
  ```bash
  testdisk /log
  ```

### **Step 2: Restore Previous Versions from Shadow Copies**
- List available shadow copies:
  ```bash
  vssadmin list shadows
  ```
- Extract previous versions:
  ```bash
  shadowcopyexplorer.exe -o recovered_files/
  ```

### **Step 3: Reconstruct a Super Timeline**
- Use Plaso to build a comprehensive forensic timeline:
  ```bash
  log2timeline.py -o timeline.plaso <disk_image>
  ```
- Convert timeline for analysis:
  ```bash
  psort.py -o CSV -w super_timeline.csv timeline.plaso
  ```

---

## 📌 4. Post-Incident Analysis
Once recovery and analysis are completed, the final phase involves reporting and improving security controls.

### **Final Report & Recommendations**
- Document forensic findings (timeline, recovered files, identified threats).
- Propose security improvements such as:
  - Implementing endpoint monitoring.
  - Enabling shadow copies for critical systems.
  - Enhancing user activity logging.

---

## 📖 5. Appendix
### **Key Artifacts and Their Locations**
| **Artifact** | **File Path** | **What It Reveals** |
|-------------|-------------|----------------------|
| Master File Table (MFT) | `$MFT` | File creation, modification, access times |
| NTFS Transaction Log | `$LogFile` | Recent file system changes |
| USN Journal | `$UsnJrnl` | Tracks all file modifications |
| Prefetch Files | `C:\Windows\Prefetch` | Program execution evidence |
| Event Logs | `C:\Windows\System32\winevt\Logs` | Security and system activity logs |

---

### 📖 Additional Resources
- [Microsoft Docs: NTFS File System](https://learn.microsoft.com/en-us/windows/win32/fileio/ntfs-file-system)
- [SANS DFIR: File Recovery Techniques](https://digital-forensics.sans.org/)
- [Autopsy File Recovery Guide](https://www.autopsy.com/)

---

## ✅ Summary
This playbook provides a structured approach to **recovering deleted files** and **reconstructing forensic timelines** using **MFT, $LogFile, Event Logs, and Shadow Copies**. By leveraging tools like **FTK Imager, Plaso, KAPE, and MFTECmd**, forensic analysts can extract critical evidence to investigate security incidents efficiently.

