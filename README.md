# Security Operations: Triage & Incident Response Portfolio

Welcome to my central **Triage and Incident Response (IR)** repository. This repository showcases hands-on cyber defense capabilities, detection engineering, security telemetry analysis, and structured incident reporting.

The projects within this repository reflect real-world SOC workflows—from raw log analysis and detection rule testing to comprehensive incident investigation and remediation guidance.

---

## 🎯 Portfolio Objectives & Focus Areas

* **Incident Investigation & Triage:** Analyzing multi-source telemetry (Windows Event Logs, Sysmon, Network PCAPs, SIEM logs) to differentiate between legitimate administrative activity and actual security breaches.
* **Detection & SIEM Engineering:** Building, testing, and tuning detection logic using **Splunk (SPL)** and standard correlation frameworks to minimize False Positives and address detection blind spots.
* **Structured Threat Intelligence & Artifact Extraction:** Extracting and defanging Indicators of Compromise (IOCs), identifying Command & Control (C2) patterns, and tracing lateral movement attempts.
* **Threat Mapping:** Framework alignment to **MITRE ATT&CK** for systematic coverage of attacker Tactics, Techniques, and Procedures (TTPs).

---

## 🧠 Investigation Methodology

Every laboratory scenario and incident report in this repository follows a rigorous, industry-aligned workflow:

1. **Telemetry & Artifact Parsing:** Extracting structural data, event IDs, network flows, and system parameters from raw log feeds.
2. **Log Classification & Relevance Determination:** Evaluating each log entry to filter out normal background noise and isolate true event indicators.
3. **IOC Extraction & Defanging:** Documenting file hashes, network IPs, domain URLs, registry modifications, and executed commands into standardized threat intelligence formats.
4. **ATT&CK Mapping:** Classifying observed adversary behaviors against the **MITRE ATT&CK Framework** (Tactic, Technique, and Sub-technique levels).
5. **Root-Cause & Timeline Reconstruction:** Reconstructing the attack sequence step-by-step to establish initial access, execution vectors, and impact scope.
6. **Reporting & Actionable Mitigation:** Authoring structured IR reports including immediate containment steps, SIEM detection recommendations, and proactive remediation.

---

## 📂 Repository Structure

```text
triage-and-ir-reporting/
│
├── labs/                        # Practical Detection & SIEM Environments
│   ├── splunk-lab-01/           # Splunk setup, log ingestion, and detection validation
│   └── ...                      # Additional lab environments
│
├── incident-reports/            # Comprehensive IR & Investigation Reports
│   ├── IR-2026-XXXX/            # Scenario-based IR analysis, timelines, and IOCs
│   └── ...
│
└── templates/                   # Standardized formats for IOCs and IR documentation