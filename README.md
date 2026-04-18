# LOTP Detection Lab - Living off the Process

## Overview
This repository contains Splunk SPL detections for the **Living off the Process (LOTP)** 
technique — a novel process injection method that avoids common EDR triggers by:

- Using existing ROP gadgets inside the target process
- Writing shellcode indirectly in 8-byte chunks via ROP chain
- Hijacking existing threads via SetThreadContext
- Reusing pre-existing RWX memory regions

Original research by: [g3tsyst3m](https://g3tsyst3m.com/lotp/Living-off-the-Process/)

## Lab Environment
- Victim: Windows (Sysmon v15.15)
- SIEM: Splunk Enterprise
- Index: dabba_windows
- Target Process: DiscordPTB.exe

## Detections
| File | Description |
|---|---|
| detections/lotp_detection.spl | 4 SPL detection rules |
| docs/MITRE_mapping.md | ATT&CK technique mapping |
| simulation/simulation_notes.md | Full simulation walkthrough |

## Key Detection Signals
1. EventID 10 - Self process injection with 0x1F3FFF access
2. EventID 10 - UNKNOWN kernel addresses in CallTrace (ROP chain)
3. EventID 1 - Calculator spawned from Discord (shellcode proof)
4. Combined rule correlating all signals

## MITRE ATT&CK
- T1055 - Process Injection
- T1106 - Native API

## Author
Suraj Deshmukh | Security Engineer | Detection Engineering
GitHub: https://github.com/Deshmukhsuraj
