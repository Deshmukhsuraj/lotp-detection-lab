# LOTP Simulation Notes

## Environment
- Attacker: Kali Linux (10.10.0.3)
- Victim: Windows ABC (10.10.0.2)
- SIEM: Splunk (dabba_windows index)
- Telemetry: Sysmon v15.15

## Target Process
- DiscordPTB.exe (PID: 7500)
- Reason: Contains mov [rax], r8; ret gadget and pre-existing RWX regions

## Gadgets Found
- ret: DiscordPTB.exe at 0x7ff776c3105f
- mov [rax], r8; ret: DiscordPTB.exe at 0x7ff777ca26e2
- pop rsp; ret: DiscordPTB.exe at 0x7ff776c51236

## RWX Regions Used
- Shellcode: 0x5934341a1000 (221184 bytes)
- Gadgets:   0x593434181000 (4096 bytes)
- Stack:     0x7ff7db080000 (4980736 bytes)

## Execution Flow
1. Found 3 ROP gadgets in DiscordPTB.exe
2. Located 5 pre-existing RWX memory regions
3. Hijacked Thread ID: 7384
4. Built ROP chain: 55 entries
5. Written 27 shellcode chunks indirectly
6. SetThreadContext: RIP=first stub, RSP=ROP chain
7. ResumeThread → shellcode executed
8. calc.exe spawned from DiscordPTB.exe ✅

## Sysmon Telemetry Captured
- EventID 10: DiscordPTB.exe self-access (0x1F3FFF)
- EventID 1: calc.exe spawned from DiscordPTB.exe
- CallTrace: UNKNOWN kernel addresses (ROP chain)
