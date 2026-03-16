# Splunk SIEM Brute Force Detection Lab

This project demonstrates a **Security Information and Event Management (SIEM) detection lab** built using **Splunk Enterprise** to detect brute-force login attempts on a Windows system.

The lab simulates a real SOC monitoring environment where Windows security logs are ingested into Splunk and analyzed using SPL queries to identify suspicious authentication activity.

---

## Lab Environment

The lab was built using **VMware Workstation** with two virtual machines:

- **Ubuntu Server** running Splunk Enterprise (SIEM)
- **Windows 11 Endpoint** generating security logs

The Windows machine forwards logs to the Splunk server where detection queries analyze authentication activity.

![VMware Lab Environment](Screenshot/vmware-lab-environment.png)

---

## Architecture Overview

The SIEM detection pipeline works as follows:

1. Windows endpoint generates **Security Event Logs**
2. Event logs contain **failed login attempts (Event ID 4625)**
3. **Splunk Universal Forwarder** sends logs to the Splunk server
4. Splunk indexes and analyzes the logs
5. A detection rule identifies **multiple failed login attempts**
6. Splunk triggers a **security alert**

---

## Detection Logic

The detection rule identifies multiple failed login attempts occurring within a short time window.

The following **Splunk Processing Language (SPL)** query was used:


sourcetype="WinEventLog:Security" EventCode=4625
| bucket _time span=5m
| stats count as failed_attempts by host, Account_Name, _time
| where failed_attempts >= 3


This query detects brute-force login attempts by identifying multiple failed authentication attempts within a **5-minute window**.

---

## Detection Query Screenshot

The screenshot below shows the detection query and results identifying failed login attempts.

![Splunk Detection Query](Screenshot/splunk-bruteforce-detection-query.png)

---

## Windows Security Event Logs

Windows records failed login attempts as **Event ID 4625** in the Security Event Log.

These logs contain valuable information including:

- Account name
- Source system
- Logon type
- Timestamp
- Failure reason

These events are forwarded to Splunk where they are analyzed for potential brute-force attacks.

![Windows Event 4625](Screenshot/windows-eventid-4625-failed-login.png)

---

## Alert Detection

When the number of failed login attempts exceeds the configured threshold, Splunk triggers an alert indicating possible brute-force activity.

The alert rule:

- Monitors failed authentication attempts
- Detects repeated login failures
- Generates a **real-time security alert**

![Splunk Triggered Alert](Screenshot/splunk-alert-triggered.png)

---

## Key Skills Demonstrated

This project demonstrates practical experience with:

- SIEM monitoring
- Splunk Enterprise configuration
- Log ingestion and analysis
- Windows Security Event Log analysis
- Splunk SPL query development
- Brute-force attack detection
- Security alerting and monitoring

---

## Tools and Technologies

- **Splunk Enterprise**
- **Splunk Universal Forwarder**
- **Windows Event Logs**
- **VMware Workstation**
- **Ubuntu Server**
- **Windows 11**

---

## Learning Outcomes

Through this project, I gained hands-on experience with:

- Building a virtual SIEM lab environment
- Ingesting endpoint logs into a SIEM
- Developing detection rules using SPL
- Investigating authentication events
- Implementing alert-based threat detection

---

## Author

**Nisarg Patel**  
Cybersecurity Graduate Student  
SOC | SIEM | Threat Detection
