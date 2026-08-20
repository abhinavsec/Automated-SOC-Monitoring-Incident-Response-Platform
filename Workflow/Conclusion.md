

## Project Outcomes

The project successfully achieved the following outcomes:

- Successfully detected security events using **Wazuh**.
- Automatically forwarded Wazuh alerts to **Shuffle SOAR** using a webhook.
- Automated alert processing and downstream actions using **Shuffle**.
- Successfully created structured security alerts in **TheHive**.
- Included alert context such as severity, source, Wazuh rule ID, tags, and MITRE ATT&CK technique.
- Successfully delivered real-time email notifications to the SOC analyst.
- Implemented an end-to-end automated alert pipeline:

```text
Wazuh → Shuffle → TheHive
              └──→ Email
```
# Conclusion

This project successfully demonstrates the implementation of an automated **Security Operations Center (SOC) alert-handling and response pipeline** using Wazuh, Shuffle SOAR, TheHive, and Email.

The workflow connects security monitoring, alert detection, security orchestration, incident management, and analyst notification into a single automated pipeline.

The implemented architecture follows this flow:

```text
Security Event
      ↓
Wazuh Detection
      ↓
Wazuh Alert
      ↓
Shuffle Webhook
      ↓
Shuffle SOAR Workflow
      ↓
   ┌───────────────┐
   │               │
   ▼               ▼
TheHive          Email
Alert             Alert
   │               │
   └───────┬───────┘
           ▼
     SOC Investigation
```
