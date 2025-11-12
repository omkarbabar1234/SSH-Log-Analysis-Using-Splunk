# 🧠 SSH Log Analysis using Splunk

### 🔍 Project Overview
This project demonstrates how to analyze SSH authentication logs using **Splunk** to detect:
- Successful logins (who connected, from where)
- Failed login attempts (possible brute-force or password spraying)
- Multiple failed authentications (brute-force indicators)
- Unauthenticated connections (possible port scanning)

---

### 🎯 Objective
To use **Splunk** as a SIEM tool for detecting and visualizing SSH activity through:
- Log ingestion and parsing  
- SPL queries for event analysis  
- Dashboards and alert configuration  

---

### ⚙️ Tools Used
- **Splunk Enterprise / Free Edition** – for log ingestion, searching, and visualization  
- **ssh_log.json** – sample dataset simulating SSH events  
- **Browser** – Splunk Web UI (Chrome / Brave)  
- **Windows/Linux** – host system for Splunk  

---

### 🧩 Implementation Steps
1. **Upload ssh_log.json** → Index: `ssh_logs`, Source type: `_json`
2. **Validate fields:**
   ```spl
   index=ssh_logs | stats count by event_type
   ```
3. **Failed login analysis**
   ```spl
   index=ssh_logs event_type="Failed SSH Login" | stats count by id.orig_h | sort - count
   ```
4. **Brute-force detection:**
   ```spl
   index=ssh_logs event_type="Multiple Failed Authentication Attempts" | stats count by id.orig_h
   ```
5. **Successful login tracking:**
   ```spl
   index=ssh_logs event_type="Successful SSH Login" | stats count by id.orig_h
   ```
6. **Unauthenticated connections:**
   ```spl
   index=ssh_logs event_type="Connection Without Authentication" | timechart count by id.orig_h
   ```
---

### 🧾 Findings
-Multiple IPs showing high failed login counts — potential brute-force attempts

-Repeated connections without authentication — likely SSH scanning

-Some IPs with both failed and successful logins — possible compromised credentials

---

### 🧠 Skills Gained

-SIEM (Splunk) Log Ingestion & Parsing     
-SPL Query Writing     
-Detection Engineering (Brute Force, Authentication Monitoring)    
-Dashboard & Alert Configuration   
-SOC Incident Analysis & Reporting  

---

### 🧾 Documentation

The detailed project report (Word format):    
SSH_Log_Analysis_Splunk_Project_BabarOmkar.docx

