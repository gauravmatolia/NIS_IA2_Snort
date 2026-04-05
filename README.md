# Network Intrusion Detection System (NIDS) using Snort

This repository documents the implementation and evaluation of **Snort**, an open-source NIDS, on a Windows environment. The project demonstrates three core functionalities: **Packet Sniffing**, **Packet Logging**, and **Rule-Based Intrusion Detection**.

## 🛠️ Prerequisites & Tools

  * **Operating System:** Windows 10/11
  * **Packet Capture Driver:** [Npcap](https://www.google.com/search?q=https://npcap.com/%23download) (Install with "WinPcap API-compatibility" enabled)
  * **IDS Engine:** [Snort 2.9.x](https://www.snort.org/downloads)
  * **Log Analysis:** [Wireshark](https://www.wireshark.org/) (Optional, for viewing .pcap logs)

-----

## 🚀 Installation & Setup

1.  **Install Npcap:** Download and run the Npcap installer. Ensure the loopback adapter is enabled if testing on a single machine.
2.  **Install Snort:** Run the Snort installer (default path: `C:\Snort`).
3.  **Configure Environment:** Add `C:\Snort\bin` to your System **Environment Variables** (Path) to run Snort from any terminal.
4.  **Directory Cleanup:** Ensure a log folder exists:
    ```powershell
    mkdir C:\Snort\log
    ```
5.  **Configure `snort.conf`:** Open `C:\Snort\etc\snort.conf` and update paths:
      * Set `ipvar HOME_NET [Your_IP_Address]`
      * Update rule paths to absolute Windows paths (e.g., `C:\Snort\rules`).

-----

## 💻 Implementation Steps

### Step 1: Interface Identification

Identify which network adapter Snort should monitor.

```powershell
snort -W
```

*Note the Index number (e.g., 4) of your active network card.*

### Step 2: Packet Sniffing Mode

Test the connection by viewing live TCP/IP headers.

```powershell
snort -v -i 4
```

### Step 3: Packet Logging Mode

Archive network traffic into the log directory for forensic analysis.

```powershell
snort -i 4 -div -l "C:\Snort\log"
```

### Step 4: IDS Mode with Custom Rules

1.  Navigate to `C:\Snort\rules\local.rules`.
2.  Add a test rule:
    `alert icmp any any -> $HOME_NET any (msg:"ICMP Packet Detected"; sid:1000001; rev:1;)`
3.  Run Snort in IDS mode:

<!-- end list -->

```powershell
snort -c C:\Snort\etc\snort.conf -i 4 -A console
```

-----

## 📊 Experimentation Results

  * **Sniffing:** Successfully captured real-time traffic headers across the NIC.
  * **Logging:** Generated binary `.pcap` files in the log folder, verified via Wireshark.
  * **Detection:** Triggered immediate console alerts upon receiving ICMP "Ping" requests, confirming the detection engine's accuracy.

-----

## 📜 Conclusion

Our team successfully demonstrated that while Sniffer and Logger modes are essential for network diagnostics, the IDS mode is the most critical for security. The ability to write custom rules allows Snort to adapt to an evolving threat landscape. Future improvements could include integrating a web-based GUI (like Snorby) or transitioning to an Inline Prevention (IPS) model to actively block malicious traffic.

-----

## 🔗 Important Links

  * **Official Snort Documentation:** [snort.org/documents](https://www.snort.org/documents)
  * **Snort Rules FAQ:** [snort.org/faq](https://www.snort.org/faq)
  * **Npcap GitHub:** [nmap/npcap](https://github.com/nmap/npcap)

-----

**Team Members:**

Member 1: Gaurav Matolia [16010123121]

Member 2: Gaurav Zope [16010123122]

Member 3: Tanmay Chinchore [16010123135]
