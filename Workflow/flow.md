
## Shuffle Automation Workflow: `Alert automation`

![shuffle_workflow](assets/workflow.png)

| Node Name | Node Type | Description & Purpose |
| :--- | :--- | :--- |
| **Webhook 1** | Trigger | Ingests real-time incoming JSON alert payloads from Wazuh. |
| **Repeat** | Flow Control | Iterates over alert arrays and parses threat telemetry fields. |
| **TheHive 1** | App Integration | Pushes structured alert data and MITRE tags to **TheHive 5** via REST API. |
| **Email** | Action | Generates and dispatches automated summary emails to the SOC team. |

## 🔍 Verified Detection Scenarios & Ingestion

### Privilege Escalation — Unauthorized Local Admin Creation
* **Source:** Wazuh
* **Type:** Privilege Escalation
* **MITRE ATT&CK Mapping:** 
  * `T1078` — Valid Accounts
  * `T1136.001` — Create Account: Local Account
* **TheHive Alert:** Logged and queued under Alerts with severity `High`.

---

## 📧 Automated SOC Notification Sample

When a high-severity alert is triggered, Shuffle formats the metadata and fires an immediate alert to analysts:

```text
Subject: [CRITICAL ALERT] Rogue Admin Account Created on windows
From: socanalyst59@gmail.com

SOC Team,

An administrative account creation event was detected by Wazuh and ingested into TheHive.

=== Incident Summary ===
Host Name: DC01
New Account: attacker
Actor (Creator): Administrator
Logon ID: 0x1ac893
Event Time: 2026-08-16T07:14:18.1799614Z

=== Action Required ===
1. Check change management tickets to confirm if this account creation was authorized.
2. If unauthorized, open the corresponding case in TheHive to disable the account.

-- Automated SOC Pipeline (Shuffle SOAR)
