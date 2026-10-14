# Alderline Payments Breach: Triage and Escalation

An incident triage exercise and the escalation report written from it. Twenty alerts from a fictional payments company reach the SOC queue on 10 March 2026. Some belong to a phishing-led intrusion, some are routine noise, and two are an unrelated incident. The Tier 1 task is to sort them out, find the attack, and hand Tier 2 a report they can act on.

Alderline Payments is invented. All hosts, accounts, domains and events are fictional.

## Contents

| File | Description |
|---|---|
| [`triage-exercise.html`](triage-exercise.html) | Interactive exercise: order the alerts, classify them, write the escalation report. Works offline in any browser. |
| [`incident-report.pdf`](incident-report.pdf) | The Tier 2 escalation report written for this case. |
| [`IOCs.md`](IOCs.md) | Indicators of compromise extracted from the report, with ATT&CK mapping and recommended searches. |

## Try the exercise

Open the exercise in the browser: [triage-exercise.html on GitHub Pages](https://elay-adar.github.io/triage-and-ir-reporting/incident-reports/alderline-payments-breach/triage-exercise.html)

Or download `triage-exercise.html` and open it locally. Answers are saved in your own browser and never leave it.

The exercise has three tasks, each unlocked by finishing the one before it:

1. **Order the alerts.** The log sources use three different time zones (UTC+3, UTC and UTC-5). Convert each time to UTC and put the alerts in chronological order.
2. **Classify the alerts.** Decide whether each alert is part of the attack, routine noise, or an unrelated incident, and give a reason based on the baseline of normal behaviour.
3. **Write the escalation report.** Executive summary, scope, timeline, findings, MITRE ATT&CK mapping, indicators of compromise, actions taken, open questions, recommendations and severity rationale. The report can be exported as a PDF.

## The incident

| Time (UTC) | Event | Tactic |
|---|---|---|
| 08:12 | Email with a macro-enabled `.docm` attachment delivered to a Finance user | Initial Access |
| 08:47 | Word starts hidden, encoded PowerShell | Execution |
| 09:15 | Scheduled task runs `svhost.exe`, a look-alike of `svchost.exe`, from a Temp folder | Persistence, Stealth |
| 09:40 | Microsoft Defender turned off through the registry | Defense Impairment |
| 10:05 | `whoami /all` and `net group "Domain Admins"` | Discovery |
| 10:30 | `rundll32.exe` reads LSASS memory | Credential Access, Stealth |
| 11:00 | RDP to the domain controller as a Domain Admin | Lateral Movement, Privilege Escalation |
| 11:20 | 412 Finance files read in 6 minutes | Collection |
| 12:00 | DNS queries with random subdomains at 340 a minute | Command and Control |
| 12:20 | SMB connection to the database server blocked | Lateral Movement (attempt) |
| 12:45 | 1.4 GB uploaded to an unsanctioned file-sharing site | Exfiltration |
| 13:10 | Shadow copy deletion on the backup server, denied | Impact (attempt) |

Severity: Critical. A Domain Admin account was compromised and financial data very likely left the company.

## Skills shown

- Correlating alerts from firewall, EDR, Windows event, proxy, email gateway, DLP and VPN sources, and normalising their time zones.
- Separating attack activity from routine noise and from an unrelated incident, using a stated baseline.
- Mapping behaviour to MITRE ATT&CK (version 20), including several tactics for one event.
- Extracting and defanging indicators of compromise.
- Writing an escalation report that separates facts from inferences and lists what was not checked.

## Notes

- ATT&CK references follow version 20. Since version 19, the former Defense Evasion tactic is split into Stealth (TA0005) and Defense Impairment (TA0112), and disabling security tools is technique T1685.
- No file hashes, decoded payloads or mail headers exist for this case, so the indicator list contains domains, paths, registry values and command lines only.
