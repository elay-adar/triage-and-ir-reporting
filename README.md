# Triage and Incident Response Reporting

Case work from my SOC Tier 1 training: alert triage, log analysis, MITRE ATT&CK mapping, indicator extraction and escalation reports.

## Cases

| Case | What it shows |
|---|---|
| [Alderline Payments Breach](incident-reports/alderline-payments-breach/) | Twenty alerts from seven log sources and three time zones. Sort them, find the phishing-led intrusion, and write the Tier 2 escalation report. Includes an interactive exercise, the report, and an IOC list. |

## How each case is worked

1. Read the baseline of normal behaviour for the servers and accounts involved.
2. Normalise the time of each alert to UTC and put the alerts in order.
3. Classify each alert as attack, routine noise, or unrelated, and state the reason.
4. Reconstruct the timeline and map the attack to MITRE ATT&CK.
5. Extract indicators of compromise and defang them.
6. Write the escalation report: what happened, what is certain, what is inferred, what was not checked, and what to do next.

## Repository layout

```text
triage-and-ir-reporting/
├── README.md
└── incident-reports/
    └── alderline-payments-breach/
        ├── README.md
        ├── triage-exercise.html
        ├── incident-report.pdf
        └── IOCs.md
```

Related work: [Northgate SOC Project](https://github.com/elay-adar/Northgate_SOC_Project), a Splunk investigation of a multi-stage intrusion.
