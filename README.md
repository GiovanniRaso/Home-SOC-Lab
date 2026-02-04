# Home SOC Lab (Blue Team) – Documentation

## Overview

This repository documents my personal **Home Security Operations Center (SOC) Lab**, built to develop hands-on skills aligned with an **entry-level SOC / Security Analyst** role. The lab focuses on **log collection, SIEM analysis, alerting, incident investigation, and documentation**, with an emphasis on explaining *why* actions are taken—not just *how*.

**Goals of this lab:**

* Gain practical experience with SIEM tools and endpoint telemetry
* Practice alert triage and basic incident response workflows
* Build repeatable detection and investigation processes
* Produce clear documentation suitable for recruiters and hiring managers

---

## Lab Architecture

### Environment Overview

The lab is built using **VirtualBox** on windows and consists of multiple virtual machines segmented into attacker, victim, and monitoring roles.

| Machine          | OS            | Purpose                       |
| ---------------- | ------------- | ----------------------------- |
| SOC Server       | Ubuntu Server | SIEM, log ingestion, alerting |
| Windows Endpoint | Windows 10    | Simulated user workstation    |
| Kali Linux       | Kali          | Attack simulation / testing   |

### Network Design

* NAT / Internal Network (isolated lab)
* All endpoints forward logs to the SOC server
* Attacker traffic is intentionally generated and monitored

*(Diagram to be added later)*

---

## Tools & Technologies

### Core Tools

* **SIEM:** Wazuh
* **Virtualization:** VirtualBox
* **Endpoint OS:** Windows 10
* **Server OS:** Ubuntu Server
* **Attack Platform:** Kali Linux

### Supporting Tools

* Sysmon (Windows telemetry)
* PowerShell (Windows event generation)
* Linux auditd (Ubuntu)
* MITRE ATT&CK Framework (mapping techniques)

---

## Setup Documentation

### 1. Virtual Machine Setup

* Installed VirtualBox on windows
* Created three VMs (Ubuntu, Windows 10, Kali Linux)
* Allocated resources:

  * Ubuntu SOC Server: 4GB RAM / 2 CPU
  * Windows Endpoint: 4GB RAM / 2 CPU
  * Kali: 2GB RAM / 2 CPU

### 2. SOC Server Configuration (Ubuntu)

* Installed Ubuntu Server
* Updated system packages
* Installed and configured Wazuh Manager
* Enabled log ingestion from endpoints

### 3. Windows Endpoint Configuration

* Installed Windows 10
* Enabled Windows Event Logging
* Installed Sysmon for enhanced telemetry
* Installed Wazuh Agent and connected to SOC server

### 4. Kali Linux Setup

* Configured attacker VM
* Installed common testing tools (nmap, metasploit)
* Verified connectivity to Windows endpoint

---

## Use Cases & Scenarios

### Scenario 1: Brute Force Login Attempt

**Objective:** Detect repeated failed login attempts on a Windows endpoint.

**Steps:**

1. Generated failed login attempts from Kali
2. Observed Windows Security Event IDs
3. Alert triggered in SIEM
4. Investigated source IP and user account

**MITRE Mapping:**

* T1110 – Brute Force

**Outcome:**

* Successfully detected authentication abuse
* Documented alert logic and investigation steps

---

### Scenario 2: Suspicious PowerShell Execution

**Objective:** Detect potentially malicious PowerShell commands.

**Steps:**

1. Executed encoded PowerShell commands
2. Captured logs via Sysmon
3. SIEM correlation rule triggered
4. Reviewed command-line artifacts

**MITRE Mapping:**

* T1059.001 – PowerShell

---

## Alert Triage Process

1. Review alert severity and description
2. Identify affected host and user
3. Validate alert with raw logs
4. Determine false positive vs true positive
5. Document findings
6. Recommend remediation

---

## Incident Response Workflow

| Phase           | Actions                      |
| --------------- | ---------------------------- |
| Identification  | Alert review, log validation |
| Containment     | Isolate host (simulated)     |
| Eradication     | Remove malicious artifact    |
| Recovery        | Restore normal operations    |
| Lessons Learned | Improve detection rules      |

---

## Detection Engineering Notes

* Custom Wazuh rules created for:

  * Failed logon thresholds
  * Suspicious PowerShell execution
  * Network scanning behavior

Future work:

* Improve signal-to-noise ratio
* Add threshold-based alert tuning

---

## Lessons Learned

* Importance of baseline behavior
* Value of enriched endpoint telemetry
* How attackers appear in logs vs theory
* SIEM tuning is iterative, not one-time

---

## Future Improvements

* Add Active Directory domain
* Integrate Suricata or Zeek
* Add email alerting
* Create dashboards for SOC metrics

---

## Repository Structure

```
/home-soc-lab
├── docs
│   ├── setup
│   ├── detections
│   ├── incidents
├── diagrams
├── screenshots
├── rules
└── README.md
```

---

## Why This Lab Matters

This project demonstrates **practical SOC skills**, including:

* SIEM deployment
* Endpoint telemetry analysis
* Alert investigation
* Clear technical documentation

It is designed to mirror **real SOC workflows** rather than CTF-style challenges.

---

## Author

**Giovanni Raso**
Computer Science | Cybersecurity | SOC Analyst Aspirant
