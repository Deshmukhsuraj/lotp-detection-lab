# MITRE ATT&CK Mapping

## Primary Technique
| ID | Name | Detection |
|---|---|---|
| T1055 | Process Injection | EventID 10 - GrantedAccess 0x1F3FFF |
| T1055.001 | Dynamic-link Library Injection | EventID 7 - ImageLoad |
| T1106 | Native API | EventID 10 - OpenProcess/SetThreadContext |

## Key APIs Monitored
| API | Sysmon Event | Access Mask |
|---|---|---|
| OpenProcess | EventID 10 | 0x1F0FFF / 0x1F3FFF |
| SetThreadContext | EventID 10 | Cross-process thread manipulation |
| WriteProcessMemory | EventID 10 | ROP chain + stub writing |
| ResumeThread | EventID 8 | Thread execution |

## Detection Coverage
| Signal | Confidence | FP Risk |
|---|---|---|
| Self-process injection 0x1F3FFF | High | Medium |
| UNKNOWN kernel CallTrace | High | Low |
| calc.exe from Discord | Critical | Very Low |
| Combined rule | Critical | Very Low |
