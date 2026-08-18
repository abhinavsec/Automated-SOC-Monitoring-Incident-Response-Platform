# Automated-SOC-Monitoring-Incident-Response-Platform
# Wazuh + Shuffle + TheHive SOAR Lab

img

## Overview

This project demonstrates a security monitoring and automated incident response pipeline built using **Wazuh, Shuffle SOAR, and TheHive**.

The lab simulates a real-world SOC workflow in which suspicious activity occurs on a Windows endpoint. Wazuh detects the activity and generates a security alert, Shuffle SOAR automatically processes the alert, TheHive creates an incident for investigation, and an email notification is delivered to the SOC analyst.

The primary detection scenario currently implemented in this project is:

> **Unauthorized Windows Account Creation**

The project focuses on demonstrating how **SIEM detection can be connected to SOAR orchestration and incident case management** to reduce manual SOC response time.

---

## Architecture

```text
                         
                         ┌─────────────────────┐
                         │  WINDOWS ENDPOINT   │
                         │        DC01         │
                         │                     │
                         │ Windows Event Logs  │
                         │       + Sysmon      │
                         │       + Wazuh Agent │
                         └──────────┬──────────┘
                                    │
                                    │ Security Telemetry
                                    ▼
                         ┌─────────────────────┐
                         │       WAZUH         │
                         │                     │
                         │  Log Collection     │
                         │  Detection Rules    │
                         │  Alert Generation   │
                         └──────────┬──────────┘
                                    │
                                    │ JSON Alert / Webhook
                                    ▼
                         ┌─────────────────────┐
                         │      SHUFFLE        │
                         │       SOAR          │
                         │                     │
                         │  Alert Processing   │
                         │  Workflow Automation│
                         └─────────┬───────────┘
                                   │
                         ┌─────────┴─────────┐
                         │                   │
                         ▼                   ▼
                ┌─────────────────┐  ┌─────────────────┐
                │     THEHIVE     │  │      EMAIL      │
                │                 │  │                 │
                │ Alert / Case    │  │ SOC Notification│
                │ Management      │  │                 │
                └─────────────────┘  └─────────────────┘
