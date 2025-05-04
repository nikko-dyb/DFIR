# Windows USB Tracking Analysis

## 📌 Overview
USB tracking in Windows involves analyzing forensic artifacts that record connected USB devices, their serial numbers, and timestamps. This is useful for identifying unauthorized device usage, data exfiltration, and insider threats.

---

## 📖 Table of Contents
- [Overview](#-overview)
- [Tools for USB Tracking Analysis](#-tools-for-usb-tracking-analysis)
- [Key USB Tracking Artifacts and Locations](#-key-usb-tracking-artifacts-and-locations)
- [Things to Notice in USB Tracking Analysis](#-things-to-notice-in-usb-tracking-analysis)
- [Limitations of USB Tracking Analysis](#-limitations-of-usb-tracking-analysis)
- [Windows USB Tracking Forensic Cheat Sheet](#-windows-usb-tracking-forensic-cheat-sheet)
- [Sample USB Tracking Analysis Files](#-sample-usb-tracking-analysis-files)
- [Additional Resources](#-additional-resources)
- [Summary](#-summary)

---

## 🛠️ Tools for USB Tracking Analysis
<details>
  <summary>Click to expand</summary>

| Tool | Description | Usage |
|------|------------|--------|
| **USBDetective** | GUI tool for analyzing USB artifacts | Interactive analysis |
| **USBDeview** | Lists all connected USB devices and history | `USBDeview.exe` |
| **RECmd (Eric Zimmerman)** | Extracts registry artifacts related to USB devices | `RECmd.exe -d SYSTEM` |
| **Volatility** | Extracts USB artifacts from memory dumps | `vol.py -f <memory_dump> printkey -K USB` |
| **FTK Imager** | Extracts and analyzes registry hives related to USB tracking | GUI-based analysis |
</details>

---

## 🔍 Key USB Tracking Artifacts and Locations
<details>
  <summary>Click to expand</summary>

| **Artifact** | **Registry Path** | **What It Reveals** |
|-------------|------------------|----------------------|
| **USB Device Entries** | `SYSTEM\CurrentControlSet\Enum\USBSTOR` | Details about connected USB storage devices |
| **Mounted Devices** | `SYSTEM\MountedDevices` | Drive letter assignments for connected USBs |
| **SetupAPI Logs** | `C:\Windows\INF\setupapi.dev.log` | Device installation logs with timestamps |
| **User Recent USB Connections** | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2` | Tracks USB devices connected to a specific user |
| **Windows Event Logs** | `C:\Windows\System32\winevt\Logs\System.evtx` | Logs related to USB device insertions and removals |
</details>

---

## ⚠️ Things to Notice in USB Tracking Analysis
- **Unauthorized USB Device Usage:** Identify devices that should not have been connected.
- **Timestamps for Insertions and Removals:** Correlate with user activity to detect suspicious behavior.
- **File Transfers and Data Exfiltration:** Check for file activity logs linked to USB drives.
- **USB Device Serial Numbers:** Can help trace specific devices to users or locations.
- **Usage Across Different Systems:** Identify USB devices used across multiple computers.

---

## 🚧 Limitations of USB Tracking Analysis
- **No File-Level Transfer Tracking:** USB artifacts do not directly record file transfers.
- **USB History May Be Cleared:** Users or malware can delete registry entries to remove evidence.
- **Limited to Connected Devices:** Only tracks devices that have been plugged into the system.
- **Time Constraints:** Some registry entries may be overwritten over time.

---

## 📜 Windows USB Tracking Forensic Cheat Sheet
<details>
  <summary>Click to expand</summary>

| **Key Data** | **Registry Path** | **Analysis Notes** |
|-------------|------------------|----------------------|
| **USB Device List** | `SYSTEM\CurrentControlSet\Enum\USBSTOR` | Shows all USB storage devices ever connected |
| **Drive Letter Assignments** | `SYSTEM\MountedDevices` | Maps USB devices to assigned drive letters |
| **User-Level USB Activity** | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\MountPoints2` | Identifies USB usage per user account |
| **Device Installation Logs** | `C:\Windows\INF\setupapi.dev.log` | Tracks when and where a USB device was installed |
</details>

---

## 📂 Sample USB Tracking Analysis Files
<details>
  <summary>Click to expand</summary>

- [Sample USB Device Registry Export](./samples/sample_usb_registry.reg)
- [USB Connection Analysis Report](./samples/usb_tracking_report.csv)
</details>

---

## 📖 Additional Resources
- [USBDetective](https://ericzimmerman.github.io/)
- [SANS DFIR: USB Forensics](https://digital-forensics.sans.org/)
- [Microsoft Docs: Windows Device Management](https://learn.microsoft.com/en-us/windows-hardware/drivers/usbcon/usb-device-features)

---

### ✅ Summary
Windows USB tracking analysis is a key forensic technique for identifying connected USB storage devices and potential data exfiltration. By using tools like USBDetective, USBDeview, and registry analysis tools, investigators can track USB activity and uncover unauthorized device usage. However, analysts should be aware of limitations, such as the inability to track file-level transfers and possible log tampering.

