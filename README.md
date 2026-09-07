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

A controlled authentication scenario was performed against the domain account `USER`.

The activity generated:

- Windows Event ID 4625 — Failed Logon
- Windows Event ID 4740 — Account Lockout

Splunk correlated three failed logon events with the subsequent account lockout and automatically triggered a scheduled alert.

**Status:** Detected and validated

📄 [View full incident report](incident-reports/INC-001-failed-logons-account-lockout.md)

---

### INC-002 — Potential Brute Force — Multiple Failed Logons

A controlled password-guessing scenario was performed against the domain account `SOC-TEST`.

Multiple Windows Event ID 4625 failed interactive logon events were generated from workstation `KOMP1`.

A Splunk detection identified accounts with five or more failed logon events within a five-minute time bucket. The detection successfully identified the simulated activity and automatically triggered a scheduled alert.

**Detection highlights:**

- Windows Event ID 4625 — Failed Logon
- Logon Type 2 — Interactive Logon
- Threshold-based detection in Splunk
- Scheduled alert execution
- Detection before account lockout

**Status:** Detected and validated

📄 [View full incident report](incident-reports/INC-002-brute-force-password-guessing.md)

---

### INC-003 — New Active Directory User Account Created

A controlled Active Directory account creation scenario was performed in the `POLICY.LAB` domain.

Windows Security Event ID 4720 was generated when a new domain user account was created. Splunk extracted both the account responsible for the change and the newly created account, then automatically triggered a scheduled alert.

**Detection highlights:**

- Windows Event ID 4720 — User Account Created
- Active Directory account change monitoring
- Creator and created account extraction using Splunk `rex`
- Scheduled alert execution
- Identity-related security monitoring

**Status:** Detected and validated

📄 [View full incident report](incident-reports/INC-003-new-ad-user-account.md)
