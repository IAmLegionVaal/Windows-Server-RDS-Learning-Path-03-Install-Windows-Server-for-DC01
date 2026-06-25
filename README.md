# Windows Server RDS Learning Path 03 — Install Windows Server for DC01

**Level:** Beginner · **Module:** 3/70

## Goal
Create the `DC01` VM and install Windows Server 2025 Desktop Experience as the clean base for the domain controller.

## Prerequisites
- `RDS-LAB-NAT` switch
- Windows Server 2025 ISO
- 2 vCPU, 4 GB RAM and 60 GB disk minimum

## Setup
1. Create a Generation 2 VM named `DC01`.
2. Connect it to `RDS-LAB-NAT` and enable Secure Boot.
3. Disable automatic checkpoints.
4. Install Windows Server 2025 Desktop Experience.
5. Set a unique local Administrator password, install updates and set the correct time zone.
6. Create a clean pre-role checkpoint.

```powershell
Get-VM DC01 | Select-Object Name,Generation,State,ProcessorCount,MemoryAssigned
Get-VMNetworkAdapter DC01 | Select-Object SwitchName,Status,MacAddress
Get-CimInstance Win32_OperatingSystem | Select-Object Caption,Version,BuildNumber
Confirm-SecureBootUEFI
Get-TimeZone
```

## Evidence
Store VM hardware, ISO source, OS edition/build, disk layout, Secure Boot result, update status and checkpoint name under `evidence/`. Record actual errors and remediation in `findings.md`.

## Troubleshooting
If the ISO does not boot, set the virtual DVD as the first boot device. For poor performance, verify host RAM pressure and SSD storage. Resolve update or component-store errors before promotion.

## Security
Verify installation media provenance, keep the VM isolated and never commit licence keys or passwords.

## Rollback
Delete only the disposable VM/VHDX if rebuilding. Retain the validated pre-role checkpoint until AD DS is deployed.

## Next
`Windows-Server-RDS-Learning-Path-04-Configure-DC01-Static-IP-and-DNS`
