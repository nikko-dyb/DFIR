# Windows Super Timeline Forensics

## 📌 Overview
A **Super Timeline** is a comprehensive forensic technique that aggregates timestamped artifacts from multiple sources to create a chronological event log. It helps investigators reconstruct user activities, system modifications, malware execution, and file access patterns.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Why Use a Super Timeline?](#-why-use-a-super-timeline)
- [Tools for Creating a Super Timeline](#-tools-for-creating-a-super-timeline)
- [Key Artifacts for Timeline Analysis](#-key-artifacts-for-timeline-analysis)
- [Building a Super Timeline](#-building-a-super-timeline)
- [Interpreting Timeline Data](#-interpreting-timeline-data)
- [Limitations of Super Timelines](#-limitations-of-super-timelines)
- [Windows Super Timeline Cheat Sheet](#-windows-super-timeline-cheat-sheet)
- [Sample Super Timeline Files](#-sample-super-timeline-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🔍 Why Use a Super Timeline?
- Provides a **holistic view** of system activity across various forensic artifacts.
- Helps **correlate user actions** with system changes and security events.
- Aids in **incident response**, **malware analysis**, and **intrusion investigations**.
- Detects **anti-forensic activities** such as timestamp manipulation or log deletion.

---

## 🛠️ Tools for Creating a Super Timeline
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **Plaso (Log2Timeline)** | Aggregates system artifacts into a super timeline | `log2timeline.py -o timeline.plaso <image>` |
| **Timesketch** | Interactive timeline visualization tool | Imports Plaso-generated timelines |
| **KAPE (Kroll Artifact Parser and Extractor)** | Collects timeline-relevant artifacts | `kape.exe --target Timelines` |
| **Sleuth Kit (mactime)** | Creates timelines from forensic images | `fls -m C: image.dd | mactime -d > timeline.csv` |
| **Volatility** | Extracts memory timestamps for timeline correlation | `vol.py -f <memory_dump> timeliner` |
</details>

---

## 🔍 Key Artifacts for Timeline Analysis
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Location** | **What It Reveals** |
|-------------|-------------|----------------------|
| **Master File Table (MFT)** | `$MFT` | File creation, modification, access times |
| **Registry Hives** | `NTUSER.DAT`, `SYSTEM`, `SOFTWARE` | System changes, user activity |
| **Windows Event Logs** | `C:\Windows\System32\winevt\Logs` | Logon/logoff, security events, system errors |
| **Prefetch Files** | `C:\Windows\Prefetch` | Application execution timestamps |
| **Shimcache & Amcache** | Registry Entries | Tracks executed programs and timestamps |
| **USB Device History** | `SYSTEM\CurrentControlSet\Enum\USBSTOR` | USB device insertion times |
| **$LogFile & $UsnJrnl** | NTFS Artifacts | File system transaction history |
| **Web History & Cache** | Browser Artifacts | User web activity timestamps |
| **Memory Artifacts** | RAM Dump | Running processes and execution history |
</details>

---

## 🔧 Building a Super Timeline
### **Step 1: Extract Data Sources**
- **Plaso/Log2Timeline**: Extracts logs, MFT, and registry artifacts
  ```bash
  log2timeline.py -o timeline.plaso <disk_image>
  ```
- **KAPE**: Targets forensic artifacts related to time-based events
  ```bash
  kape.exe --target Timelines --output timeline.csv
  ```
- **Volatility (For Memory Artifacts)**:
  ```bash
  vol.py -f memory.raw timeliner
  ```

### **Step 2: Convert to Readable Format**
- Convert Plaso output to CSV for further analysis:
  ```bash
  psort.py -o CSV -w super_timeline.csv timeline.plaso
  ```

### **Step 3: Visualize with Timesketch**
- Upload `super_timeline.csv` to Timesketch for interactive analysis.

---

## 📊 Interpreting Timeline Data
- **Correlate events across multiple artifacts** (e.g., logins, file access, malware execution).
- **Look for anomalies** such as rapid file modifications or abnormal execution sequences.
- **Identify anti-forensic actions**, such as deleted logs or modified timestamps.
- **Reconstruct a clear incident timeline** by aligning artifacts with known attack patterns.

---

## 🚧 Limitations of Super Timelines
- **Data Overload:** Large timelines can contain millions of entries, requiring filtering.
- **Timestamps May Be Manipulated:** Attackers may alter MACB timestamps.
- **Contextual Gaps:** Some actions may not be logged, requiring correlation with additional evidence.
- **Performance Issues:** Parsing and analyzing large datasets can be resource-intensive.

---

## 📜 Windows Super Timeline Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Command** | **Tool** | **Description** |
|------------|--------|----------------|
| `log2timeline.py -o timeline.plaso <image>` | Plaso | Creates timeline from forensic image |
| `psort.py -o CSV -w timeline.csv timeline.plaso` | Plaso | Converts timeline to CSV format |
| `fls -m C: image.dd | mactime -d > timeline.csv` | Sleuth Kit | Extracts MAC times from forensic image |
| `vol.py -f <memory_dump> timeliner` | Volatility | Extracts timestamps from memory dumps |
</details>

---

## 📂 Sample Super Timeline Files
<details>
  <summary>Click to expand</summary>

- [Sample Super Timeline CSV](./samples/sample_super_timeline.csv)
- [Plaso Processed Timeline](./samples/plaso_timeline.plaso)
</details>

---

## 📖 Additional Resources
- [Plaso Documentation](https://plaso.readthedocs.io/en/latest/)
- [SANS DFIR: Super Timelines](https://digital-forensics.sans.org/)
- [Timesketch: Interactive Timeline Analysis](https://github.com/google/timesketch)

---

### ✅ Summary
Super timelines consolidate forensic artifacts from various sources to reconstruct system events with high precision. By leveraging tools like **Plaso**, **Timesketch**, and **Volatility**, forensic investigators can uncover hidden activities, track malware execution, and enhance incident response capabilities. However, challenges such as data overload and timestamp manipulation must be considered.

