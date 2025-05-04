# Windows Memory Forensics

## 📌 Overview
Memory forensics is the process of analyzing volatile memory (RAM) to uncover artifacts related to running processes, network connections, malware, and system activity. It is a critical component in digital investigations, helping analysts detect hidden threats, rootkits, and active intrusions.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for Memory Forensics](#-tools-for-memory-forensics)
- [Key Memory Artifacts and Analysis](#-key-memory-artifacts-and-analysis)
- [Things to Notice in Memory Forensics](#-things-to-notice-in-memory-forensics)
- [Limitations of Memory Forensics](#-limitations-of-memory-forensics)
- [Windows Memory Forensic Cheat Sheet](#-windows-memory-forensic-cheat-sheet)
- [Sample Memory Analysis Files](#-sample-memory-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for Memory Forensics
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **Volatility Framework** | Extracts and analyzes memory artifacts | `vol.py -f <memory_dump> <plugin>` |
| **Rekall** | Advanced memory analysis framework | `rekal -f <memory_dump>` |
| **MemProcFS** | Mounts memory dumps as a file system for analysis | `memprocfs.exe <memory_dump>` |
| **WinDBG** | Microsoft debugger for advanced memory forensics | `windbg -z <memory_dump>` |
| **FTK Imager** | Acquires memory dumps and performs basic analysis | GUI-based analysis |
</details>

---

## 🔍 Key Memory Artifacts and Analysis
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Analysis Method** | **What It Reveals** |
|-------------|------------------|----------------------|
| **Running Processes** | `vol.py -f <dump> pslist` | Active processes and parent-child relationships |
| **Network Connections** | `vol.py -f <dump> netscan` | Open network connections and remote communication |
| **DLL and Code Injection** | `vol.py -f <dump> malfind` | Hidden or injected malicious code |
| **User Sessions** | `vol.py -f <dump> logonsessions` | Active and historical user logins |
| **Browser and Credential Data** | `vol.py -f <dump> chromehistory` | Extracts browser artifacts from memory |
</details>

---

## ⚠️ Things to Notice in Memory Forensics
- **Suspicious Processes:** Look for uncommon parent-child process relationships.
- **Hidden Malware:** Memory-resident malware may not exist on disk but can be found in RAM.
- **Credential Theft:** Attackers often use memory scraping to extract plaintext passwords.
- **Remote Access Trojans (RATs):** Identify suspicious remote connections in network logs.
- **Memory Artifacts of Fileless Malware:** Malicious code executing directly in memory without being written to disk.

---

## 🚧 Limitations of Memory Forensics
- **Requires a RAM Dump:** Live memory must be acquired before system shutdown.
- **Potentially Large Datasets:** Memory dumps can be several gigabytes in size, making analysis time-consuming.
- **Encrypted Memory Sections:** Some regions of memory may be encrypted or inaccessible.
- **Anti-Forensic Techniques:** Malware can attempt to hide itself in memory or overwrite key artifacts.

---

## 📜 Windows Memory Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Command** | **Tool** | **Description** |
|------------|--------|----------------|
| `vol.py -f <dump> pslist` | Volatility | Lists running processes |
| `vol.py -f <dump> psscan` | Volatility | Finds hidden and terminated processes |
| `vol.py -f <dump> netscan` | Volatility | Displays active network connections |
| `vol.py -f <dump> dumpfiles` | Volatility | Extracts files from memory |
| `vol.py -f <dump> malfind` | Volatility | Detects injected malicious code |
</details>

---

## 📂 Sample Memory Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample Memory Dump](./samples/sample_memory_dump.raw)
- [Memory Analysis Report](./samples/memory_analysis_report.csv)
</details>

---

## 📖 Additional Resources
- [Volatility Framework](https://github.com/volatilityfoundation/volatility3)
- [SANS DFIR: Memory Forensics](https://digital-forensics.sans.org/)
- [Microsoft Docs: Windows Debugging](https://learn.microsoft.com/en-us/windows-hardware/drivers/debugger/debugger-download-tools)

---

### ✅ Summary
Memory forensics is an essential technique in digital investigations, providing insights into active processes, network activity, and hidden malware. By using tools like Volatility, Rekall, and WinDBG, investigators can uncover vital forensic evidence stored in RAM. However, challenges such as anti-forensic measures and large dataset analysis must be considered.

