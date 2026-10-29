# Linux & Data Center Home Lab 

A personal VirtualBox lab for practicing Linux administration,
infrastructure monitoring, and incident troubleshooting.

## Lab Environment

- CentOS Stream 10 servers for Linux administration.
- pfSense for routing and gateway services.
- Windows Server for Active Directory and DNS.
- Zabbix for infrastructure monitoring and alerting.
- Zammad for incident ticket management.

## Practical Skills

- Linux service troubleshooting with systemctl and journalctl.
- LVM, filesystems, permissions, and SELinux.
- Bash scripts, automated backups, and systemd timers.
- Rootless Podman containers.
- Monitoring alerts and incident documentation.

## Incident Workflow

Simulate a failure → detect it with Zabbix → track it in Zammad →
investigate → fix → verify recovery.

All incidents documented here are lab simulations.


## Incident Reports

- [Incident 001 — Apache HTTPD Configuration Error](incidents/001-httpd-configuration-error.md)
