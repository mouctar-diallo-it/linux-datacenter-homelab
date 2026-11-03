
# Incident 004 — Critical Disk Space on /data/applications

## Issue

Zabbix detected critically low available disk space on the `/data/applications` filesystem on `server01`.

- Host: `server01.dclab.local`
- Severity: Average
- Zabbix Problem ID: 2971
- Filesystem: `/data/applications`

## Detection

Zabbix generated the following alert:

Linux: FS [/data/applications]: Space is critically low`

The monitoring system reported disk usage above 90%.

Operational data showed approximately 94.2% disk usage.

## Investigation

Filesystem usage was verified directly on `server01`:

```bash
- Post-resolution verification
df -h /data/applications
```
Result:
Size: 3.9G
Used: 3.7G
Available: 229M
Use: 95%

The largest files were then identified:
find /data/applications -type f -exec du -h {} + | sort -hr | head -n 20

A 3.5 GB file was identified:
3.5G /data/applications/incident004-fill.dat

The file was checked with lsof to determine whether it was actively opened by a process:
lsof /data/applications/incident004-fill.dat

No process was found actively using the file.
Root Cause
A 3.5 GB file named incident004-fill.dat consumed most of the available space on the /data/applications filesystem.

This caused filesystem utilization to increase to approximately 95%, triggering the Zabbix alert.
Resolution
After confirming the file was the source of the disk-space problem and was not actively being used, it was removed:
rm /data/applications/incident004-fill.dat

## Verifications
The filesystem was checked again:
df -h /data/applications

Disk utilization returned to normal:
Size: 3.9G
Used: 108M
Available: 3.8G
Use: 3%

The problematic file was also confirmed to no longer exist.
Monitoring Verification
Zabbix automatically detected the recovery and changed the incident status from:

PROBLEM → RESOLVED

The recovery notification confirmed resolution of Zabbix Problem ID 2971.

## Skills Demonstrated
- Linux filesystem troubleshooting
- Disk capacity monitoring
- df disk utilization analysis
- find, du, and sort disk investigation
- Open-file investigation with lsof
- Root cause analysis
- Zabbix monitoring
- Incident remediation

