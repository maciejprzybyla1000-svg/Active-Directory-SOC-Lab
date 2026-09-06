# Active Directory SOC Lab

A hands-on cybersecurity lab focused on Windows Active Directory
monitoring, log collection, SIEM analysis and detection engineering.

The environment was built using Windows Server 2019, Windows 10,
Splunk Enterprise and Splunk Universal Forwarder.

The goal of this project is to simulate common security events in an
Active Directory environment, investigate them from a SOC analyst's perspective
and build detection rules in Splunk.

## Lab Architecture

- Windows Server 2019 — Active Directory Domain Controller
- Windows 10 — Domain workstation (KOMP1)
- Splunk Enterprise — SIEM server
- Splunk Universal Forwarder — Windows Security Event collection
- Domain — POLICY.LAB

## Current Detection Scenarios

### INC-001 — Repeated Failed Logons Leading to Account Lockout

A controlled authentication scenario was performed against the
domain account `USER`.

The activity generated:

- Windows Event ID 4625 — Failed Logon
- Windows Event ID 4740 — Account Lockout

Splunk correlated three failed logon events with the subsequent
account lockout and automatically triggered a scheduled alert.

Status: Detected and validated
