# 🛡️ SOC Incident Response & Log Analysis Lab

A comprehensive, interactive Incident Response (IR) and Log Analysis lab. This project simulates an enterprise cyber attack scenario, guiding SOC analysts through initial alert triage, IOC identification, baseline noise filtering, and MITRE ATT&CK mapping up to a final Tier-2 investigation report.

---

## 📁 Repository Structure

| File / Module | Description |
| :--- | :--- |
| **`Landing-Page.html`** | Overview of the simulated target organization, including internal network architecture, baseline operational norms, and the raw alert queue. |
| **`Try-It-Yourself.html`** | Interactive study guide and hands-on lab featuring guided tasks, log exercises, and dynamic verification answers. |
| **`Log-analysis-and-triage.html`** | Detailed technical analysis breaking down true positives vs. false positives/noise and mapping malicious activity. |
| **`Tier2-Report.pdf`** | Official SOC Tier-2 Incident Investigation Report summarizing key takeaways, evidence, and remediation steps. |

---

## 🔍 Attack Scenario Highlights

The investigation covers a multi-stage intrusion lifecycle across an enterprise environment:

1. **Initial Access (`T1566.001`):** Phishing email carrying a weaponized `.docm` attachment with embedded VBA macros.
2. **Execution & Evasion (`T1059.001`, `T1562.001`):** PowerShell execution with hidden flags (`-nop -w hidden -enc`) and Windows Defender tampering via Registry manipulation.
3. **Persistence (`T1053.005`, `T1036.005`):** Masquerading binary (`svhost.exe` inside local `AppData\Temp`) scheduled at user logon.
4. **Credential Access & Discovery (`T1003.001`, `T1069.002`):** Active Directory group enumeration (`net group "Domain Admins"`) and LSASS memory dumping via `rundll32.exe`.
5. **Lateral Movement & Exfiltration (`T1021.001`, `T1071.004`, `T1567.002`):** Unauthorized RDP to the Domain Controller using stolen high-privilege credentials, automated file collection, DNS Tunneling C2, and HTTPS exfiltration to cloud storage.
6. **Impact (`T1490`):** Shadow Copy deletion (`vssadmin.exe delete shadows /all /quiet`) to impede recovery.

---

## 🚀 How to Use

1. **Clone the repository:**
   ```bash
  git clone https://github.com/elay-adar/triage-and-ir-reporting.git
  cd triage-and-ir-reporting
