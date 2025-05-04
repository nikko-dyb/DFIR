# Windows File Recovery Fundamentals

## 📌 Overview
File recovery is a crucial forensic process aimed at retrieving lost, deleted, or corrupted files. This process leverages forensic artifacts such as the **Master File Table (MFT)**, **$LogFile**, and **$Recycle.Bin** to reconstruct file data. Understanding the mechanisms behind file deletion and recovery can help digital forensics professionals recover evidence even after an attempt to erase it.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [How File Deletion Works](#-how-file-deletion-works)
- [Tools for File Recovery](#-tools-for-file-recovery)
- [Recovering Files Using MFT](#-recovering-files-using-mft)
- [Other Methods for File Recovery](#-other-methods-for-file-recovery)
- [Limitations of File Recovery](#-limitations-of-file-recovery)
- [Windows File Recovery Cheat Sheet](#-windows-file-recovery-cheat-sheet)
- [Sample File Recovery Scenarios](#-sample-file-recovery-scenarios)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🔍 How File Deletion Works
When a file is deleted in Windows:
1. The **Master File Table (MFT)** entry remains but is marked as unallocated.
2. The file contents remain on disk until they are overwritten.
3. The **$LogFile** (NTFS transaction log) may retain references to file changes.
4. The **$Recycle.Bin** temporarily stores files before permanent deletion (if not shift-deleted).
5. **Shadow copies** (if enabled) may retain file snapshots.

---

## 🛠️ Tools for File Recovery
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **FTK Imager** | Extracts and analyzes file system data | GUI-based recovery |
| **Autopsy (Sleuth Kit)** | Open-source forensic suite for file recovery | Interactive analysis |
| **TestDisk** | Recovers lost partitions and deleted files | `testdisk` CLI interface |
| **Recuva** | User-friendly file recovery tool | GUI-based recovery |
| **X-Ways Forensics** | Advanced forensic suite for deep file recovery | Interactive file system analysis |
</details>

---

## 🔍 Recovering Files Using MFT
The **MFT (Master File Table)** stores metadata for each file, making it a powerful source for file recovery. Here’s how to recover files using MFT:

### **Step 1: Extract the MFT**
```bash
mftrcrd.exe -i C:\$MFT -o mft_dump.csv
```

### **Step 2: Analyze MFT Entries**
```bash
analyzeMFT.py -f mft_dump.csv -o recovered_files.csv
```

### **Step 3: Recover File Data**
Using **FTK Imager**:
1. Open FTK Imager and load the drive image.
2. Navigate to `$MFT` and locate unallocated entries.
3. Extract file contents manually or via scripting.

---

## 🔍 Other Methods for File Recovery
<details>
  <summary>Click to expand</summary>

| **Method** | **Technique** | **Use Case** |
|-----------|-------------|-------------|
| **Shadow Copies** | Restore previous versions | If Volume Shadow Copy is enabled |
| **$LogFile Analysis** | NTFS transaction log recovery | Recover file system changes |
| **RAW Carving** | Extracting file signatures manually | Useful when MFT is damaged |
| **File Carving** | Signature-based recovery (e.g., JPEG, DOCX) | For fragmented or partially overwritten files |
</details>

---

## 🚧 Limitations of File Recovery
- **Overwritten Data Cannot Be Recovered**: If new data is written over a deleted file, recovery is impossible.
- **SSD TRIM Feature Erases Data Quickly**: On SSDs, TRIM permanently deletes unallocated space.
- **Encrypted Files May Be Unrecoverable**: BitLocker or EFS encryption can render deleted files inaccessible.
- **File Fragmentation Complicates Recovery**: Large or fragmented files may only be partially recoverable.

---

## 📜 Windows File Recovery Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Key Data** | **File System Artifact** | **Recovery Potential** |
|-------------|------------------|----------------------|
| **Deleted Files** | `$MFT` | High if not overwritten |
| **Recent Modifications** | `$LogFile` | Can help reconstruct edits |
| **Old Versions** | Shadow Copies | Useful for system snapshots |
| **File Names & Paths** | `$MFT` | Names can persist after deletion |
</details>

---

## 📂 Sample File Recovery Scenarios
<details>
  <summary>Click to expand</summary>

- [Sample MFT Extraction](./samples/sample_mft_extract.csv)
- [Recovered File Report](./samples/recovered_files_report.csv)
</details>

---

## 📖 Additional Resources
- [Microsoft Docs: NTFS File System](https://learn.microsoft.com/en-us/windows/win32/fileio/ntfs-file-system)
- [SANS DFIR: File Recovery Techniques](https://digital-forensics.sans.org/)
- [Autopsy File Recovery Guide](https://www.autopsy.com/)

---

### ✅ Summary
Windows file recovery relies on forensic techniques to extract deleted or lost files using artifacts like the **MFT**, **$LogFile**, and **Shadow Copies**. By leveraging tools like FTK Imager, Autopsy, and TestDisk, investigators can reconstruct file histories and recover valuable evidence. However, file recovery is subject to limitations such as overwriting, SSD TRIM effects, and encryption barriers.

