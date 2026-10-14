# Indicators of Compromise

**Case:** ALDERLINE-2026-0310 | **Incident:** Phishing leading to data theft from the Finance share
**Organisation:** Alderline Payments (fictional) | **Date of activity:** 10 March 2026 | **Severity:** Critical

This file lists the indicators extracted from the [incident report](incident-report.pdf) so another team can search for them. All times are UTC. Domains and email addresses are defanged: each `.` before the top-level domain is written `[.]`.

No file hashes, decoded PowerShell command or malware sample were available during triage. Indicators that depend on them are listed as open work at the end.

## Summary

| Type | Count |
|---|---|
| Domains | 3 |
| Email artefacts | 2 |
| File artefacts | 2 |
| Registry artefacts | 1 |
| Command lines | 3 |
| Process behaviour | 1 |

## Network indicators

| Indicator | Role | First seen (UTC) | Ticket | ATT&CK |
|---|---|---|---|---|
| `invoice-verify-secure[.]com` | Phishing sender domain | 08:12 | 8 | T1566.001 |
| `update-cdn-relay[.]net` | Command and control, DNS tunnelling | 12:00 | 18 | T1071.004, T1572 |
| `*.update-cdn-relay[.]net` | Randomised subdomains used by the tunnel, 340 queries a minute | 12:00 | 18 | T1071.004, T1572 |
| `filebin-share[.]net` | Exfiltration destination, 1.4 GB uploaded over HTTPS (POST) | 12:45 | 3 | T1567.002 |

Example subdomain from the log: `8f2ac91e0b[.]update-cdn-relay[.]net`

## Email indicators

| Indicator | Role | Ticket | ATT&CK |
|---|---|---|---|
| `billing-support@invoice-verify-secure[.]com` | Sender address | 8 | T1566.001 |
| `Invoice_48213.docm` | Macro-enabled attachment, delivered to `y.cohen` | 8 | T1566.001, T1204.002 |

## Host indicators

| Type | Indicator | Context | Ticket | ATT&CK |
|---|---|---|---|---|
| File path | `C:\Users\ycohen\AppData\Local\Temp\svhost.exe` | Runs from a Temp folder. The name imitates `svchost.exe` | 16 | T1036.005 |
| Scheduled task | `\Microsoft\Windows\WinUpdateCheck` | Runs `svhost.exe` at logon. The name imitates a Windows update task | 16 | T1053.005, T1036.005 |
| Registry value | `HKLM\SOFTWARE\Policies\Microsoft\Windows Defender\DisableAntiSpyware = 1` | Set by `powershell.exe` (PID 4820) | 13 | T1112, T1685 |

## Command lines and process behaviour

| Indicator | Context | Ticket | ATT&CK |
|---|---|---|---|
| `powershell.exe -nop -w hidden -enc <base64>` | Parent process `WINWORD.EXE` on `WKS-YCOHEN`. Payload was truncated in the alert | 5 | T1204.002, T1059.001 |
| `whoami /all && net group "Domain Admins" /domain` | Run through `cmd.exe` on `WKS-YCOHEN` | 19 | T1033, T1069.002 |
| `vssadmin.exe delete shadows /all /quiet` | Run as `svc_backup` from `10.10.2.45` on BKP01. Result: Access Denied | 11 | T1490 |
| `rundll32.exe` opening `lsass.exe` with a MiniDump access pattern | Credential dumping. Detection rule EDR-0891 | 10 | T1003.001, T1218.011 |

## Affected assets

These are victims, not indicators. Do not block them. Use them to scope the search.

| Asset | Type | Involvement |
|---|---|---|
| `WKS-YCOHEN` (10.10.2.45) | Workstation | First host infected, source of all attacker activity |
| `DC01` (10.10.1.10) | Domain controller | RDP session as `admin_dana` from `WKS-YCOHEN` |
| `FS01` (10.10.1.20) | File server | 412 files read from `\\FS01\Finance$` in 6 minutes |
| `DB01` (10.10.1.30) | Database server | SMB connection attempt blocked by FW-SEG-114 |
| `BKP01` (10.10.1.40) | Backup server | Shadow copy deletion attempt, denied |
| `y.cohen` | User account | Received the phishing email |
| `ALDERLINE\admin_dana` | Domain Admin account | Used from the compromised workstation |
| `svc_backup` | Service account | Used from the compromised workstation |

## Recommended searches

1. Search mail logs for the sender domain `invoice-verify-secure[.]com` and the attachment name `Invoice_48213.docm` to find other recipients.
2. Search DNS and proxy logs for `update-cdn-relay[.]net` and `filebin-share[.]net` across all hosts.
3. Search endpoint telemetry for `svhost.exe` and the scheduled task `\Microsoft\Windows\WinUpdateCheck`.
4. Search EDR for `WINWORD.EXE` spawning `powershell.exe`, and for `rundll32.exe` opening `lsass.exe`.
5. Check the Windows Defender policy registry key on all workstations for `DisableAntiSpyware = 1`.

## Not yet available

- SHA-256 hash of `Invoice_48213.docm` and `svhost.exe`
- Decoded PowerShell command from the `-enc` payload
- Source IP and mail headers of the phishing email
- Resolved IP addresses behind `update-cdn-relay[.]net` and `filebin-share[.]net`

These need memory and disk forensics on `WKS-YCOHEN` and the original email, which are open items in the report (sections 8 and 9).
