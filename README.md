# Splunk SIEM Brute Force Detection Lab

This project demonstrates a Splunk SIEM lab built in VMware to detect Windows brute-force login attempts.

---

## Lab Environment

VMware Workstation  
Ubuntu Splunk Server  
Windows 11 Endpoint

---

## Detection Logic

Failed login attempts generate **Event ID 4625**.

SPL Query:
