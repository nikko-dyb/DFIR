# Classification: Public

# Windows Memory Forensics Playbook

## 📌 Preface
This playbook provides a structured approach for conducting **Windows memory forensics** investigations. It is designed for **forensic analysts, incident responders, and SOC teams** to extract, analyze, and interpret volatile memory artifacts for identifying malware, insider threats, and attack traces.

## 📖 Table of Contents
1. Overview
2. General Memory Forensics Workflow
3. Scenario 1: Detecting Malware in Memory
4. Scenario 2: Investigating Credential Theft
5. Scenario 3: Identifying Remote Access Trojans (RATs)
6. Post-Investigation Actions
7. Appendix

---

## 🔍 1. Overview
Windows memory forensics involves capturing and analyzing RAM to uncover **running processes, injected malware, network connections, and credential theft techniques**. Since memory is volatile, proper acquisition and rapid analysis are critical.

### **Key Objectives:**
- **Capture a forensic memory dump** from a live system.
- **Analyze processes, DLLs, and network connections** in RAM.
- **Detect fileless malware and injected code** that may not exist on disk.
- **Extract credentials and persistence mechanisms** used by attackers.
- **Correlate memory findings with event logs and other forensic artifacts.**

---

## 🔄 2. General Memory Forensics Workflow
1. **Acquire memory image from a live system.**
2. **Verify memory integrity and extract artifacts.**
3. **Analyze processes, DLLs, network activity, and registry data.**
4. **Detect malware, suspicious scripts, or injected code.**
5. **Extract credentials or persistence techniques used by attackers.**
6. **Correlate findings with host and network logs.**

---

## 📌 3. Scenario 1: Detecting Malware in Memory

### **Objective:** Identify and extract malware running in volatile memory.

### **Workflow:**
1. **Memory Acquisition**
   - Use **WinPMEM** to acquire memory dump:
     ```bash
     winpmem.exe -o memory_dump.raw
     ```
   - Validate memory integrity:
     ```bash
     sha256sum memory_dump.raw > hash.txt
     ```
2. **Process & DLL Analysis**
   - List running processes:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 pslist
     ```
   - Identify suspicious processes with unusual parent-child relationships:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 pstree
     ```
   - Scan for malicious DLLs:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 dlllist -p <PID>
     ```
3. **Malicious Code Injection Detection**
   - Detect injected code segments:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 malfind -p <PID>
     ```
4. **Network Connection Analysis**
   - Identify active network connections:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 netscan
     ```
   - Extract open ports linked to suspicious processes.
5. **Dump and Analyze Malware Samples**
   - Extract suspicious executables:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 procdump -p <PID> -D ./malware/
     ```
   - Upload to **VirusTotal** or analyze in **CAPE Sandbox**.
6. **Document Findings & Report Analysis**
   - Summarize identified malware behaviors and persistence mechanisms.

---

## 📌 4. Scenario 2: Investigating Credential Theft

### **Objective:** Identify credential harvesting techniques used by attackers.

### **Workflow:**
1. **Extract LSASS Memory for Credential Dumping**
   - Dump **LSASS** process:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 memdump -p lsass.exe -D ./dumps/
     ```
   - Analyze with **Mimikatz**:
     ```bash
     mimikatz.exe "sekurlsa::minidump lsass.DMP" "sekurlsa::logonPasswords full" exit
     ```
2. **Check for SAM & SYSTEM Registry Dumps**
   - Extract registry hives from memory:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 hivelist
     ```
   - Extract and analyze **SAM database**:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 hashdump
     ```
3. **Detect Credential Theft Tools in Memory**
   - Scan for **Mimikatz-like behavior**:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 malfind
     ```
4. **Document Findings & Report Analysis**
   - List compromised user credentials and escalation techniques.

---

## 📌 5. Scenario 3: Identifying Remote Access Trojans (RATs)

### **Objective:** Detect unauthorized remote access sessions running in memory.

### **Workflow:**
1. **Scan for Suspicious Processes**
   - Identify processes with unusual network activity:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 pslist | grep svchost
     ```
   - Check running services:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 svcscan
     ```
2. **Analyze Network Connections**
   - Identify external C2 connections:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 netscan
     ```
   - Compare with known **C2 Indicators of Compromise (IOCs)**.
3. **Detect Persistence Mechanisms**
   - Check **scheduled tasks**:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 schedscan
     ```
   - Analyze **registry-based persistence**:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 printkey -K "Software\Microsoft\Windows\CurrentVersion\Run"
     ```
4. **Dump and Reverse Engineer the RAT**
   - Extract executable for sandbox analysis:
     ```bash
     volatility -f memory_dump.raw --profile=Win10x64 procdump -p <PID> -D ./RAT_samples/
     ```
5. **Document Findings & Report Analysis**
   - Summarize RAT behavior and mitigation steps.

---

## 🔄 6. Post-Investigation Actions
- **Validate collected intelligence before acting.**
- **Follow chain of custody guidelines for evidence handling.**
- **Collaborate with law enforcement where required.**
- **Store findings in a secure repository for future reference.**

---

## 📖 7. Appendix
### **Memory Forensics Tool Reference**
| **Tool** | **Purpose** | **Link** |
|---------|------------|----------|
| Volatility | Memory analysis | [Volatility Foundation](https://www.volatilityfoundation.org/) |
| WinPMEM | Memory acquisition | [Download](https://github.com/Velocidex/WinPmem) |
| Mimikatz | Credential dumping | [GitHub](https://github.com/gentilkiwi/mimikatz) |

---

## ✅ Summary
This playbook provides a structured methodology for **Windows memory forensics**, covering malware detection, credential theft analysis, and RAT identification. By leveraging **Volatility, Mimikatz, and network forensic tools**, investigators can uncover in-memory threats and take appropriate mitigation steps.

