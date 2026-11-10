# 🛡️ Splunk SIEM & Threat Detection Lab

## 📌 Project Overview
An end-to-end security monitoring lab demonstrating SIEM deployment using Splunk Enterprise, log aggregation via Splunk Universal Forwarder, and real-time threat detection and analysis of a simulated SMB Brute Force Attack launched from Kali Linux.

## 🏗️ Environment Architecture
* **SIEM Host:** Splunk Enterprise running on Windows 11.
* **Target Endpoint:** Windows 10 Virtual Machine configured with Sysmon and Splunk Universal Forwarder.
* **Attacker Machine:** Kali Linux executing automated brute-force attacks via THC-Hydra.
* **Network Integration:** Custom inbound firewall rules configured on TCP Port 9997 for indexer communication.

## ⚔️ Attack Simulation & Detection Logic
* **Vector:** SMB Login Brute Force against target endpoint (192.168.1.128).
* **Tool Used:** `hydra -l Administrator -P /usr/share/wordlists/rockyou.txt smb://192.168.1.128`
* **Telemetry Collected:** Windows Security Event Log EventCode 4625 (An account failed to log on).
* **SPL Query:**
  ```spl
  index=main EventCode=4625

## 🔍 Alert & Incident Analysis
* **Alert Name:** Brute Force Detected
* **Severity:** High
* **Detection Trigger:** Configured a real-time Splunk alert to trigger when EventCode=4625 exceeds 5 failed attempts within a 5-minute window.
* **Analyst Triage:** Successfully evaluated the triggered high-severity alerts to differentiate between automated brute-force attempts and normal authentication errors, identifying indicators of compromise (IoCs).


<img width="3840" height="2400" alt="attack (hydra)" src="https://github.com/user-attachments/assets/042a2d02-a91d-4bd4-85e1-25034eb0b0a2" />
<img width="3840" height="2400" alt="triggered alert" src="https://github.com/user-attachments/assets/d6a7c067-5c6e-44a9-ad31-656cab80948b" />
