# 🔐 Brute Force Attack Simulation Lab

## What Was Done

In this lab, a brute-force attack simulation was performed against a Windows endpoint to test Wazuh’s ability to detect repeated failed login attempts. Multiple failed SMB authentication attempts were executed from a Kali Linux machine targeting a Windows host. Before simulating the attack, network connectivity and port accessibility were verified to ensure traffic would reach the target. The Windows Event Logs were monitored, and Wazuh was used to detect individual failures and correlate multiple failed attempts into a high-severity alert.

---

## How The Lab Was Done

1. **Environment Setup**  
   - Kali Linux as the attacker machine  
   - Windows 10 as the target endpoint  
   - Wazuh Agent installed on Windows and connected to Wazuh Manager  

2. **Connectivity and Port Validation**  
   - Verified that Kali could reach Windows over the network (ping test)  
   - Confirmed Windows Firewall allowed inbound traffic or temporarily disabled it for lab purposes  
   - Checked which ports were open using `nmap`, ensuring SMB (port 445) was accessible  

3. **Simulating the Attack**  
   - Used `smbclient` on Kali to attempt SMB logins:  
     ```bash
     smbclient -L //10.10.0.4 -U Admin
     ```  
   - Entered multiple incorrect passwords to generate authentication failures  
   - A total of 8 failed login attempts were performed  

4. **Log Validation**  
   - Checked Windows Event Viewer → Security logs  
   - Confirmed Event ID: **4625** entries for failed logons  
   - Verified Logon Type 3 (Network), failure reason, and source IP  

5. **SIEM Detection**  
   - Wazuh ingested Windows Security logs  
   - Individual failed logins triggered rule **60122** (level 5)  
   - Repeated failures triggered rule **60204** (level 10), indicating a brute-force attack  

---

## Findings

- Windows generated Event ID 4625 for each failed login attempt.  
- Wazuh successfully collected and parsed the logs.  
- Base detection rules (60122) triggered for each failure.  
- Correlation rules (60204) escalated the alert when repeated failures occurred.  
- Frequency-based detection logic worked as expected.  
- MITRE ATT&CK T1110 (Brute Force) was mapped successfully.  

---

## Lessons Learned

- Always verify connectivity and port accessibility before attempting attacks; blocked traffic prevents detection events.  
- Frequency-based correlation rules prevent alert fatigue by escalating only repeated malicious behavior.  
- Manual SMB authentication failures are sufficient to test brute-force detection pipelines.  
- Validating log ingestion and ensuring agent connectivity is essential before testing detection rules.  
- Understanding rule thresholds (e.g., `$MS_FREQ`) is critical to interpret when alerts are triggered.  
- SOC detection pipelines require end-to-end validation: attack → log → ingestion → correlation → alert.  
