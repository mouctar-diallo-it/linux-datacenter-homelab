# Incident 001 — Apache HTTPD Configuration Error

## Environment

- Personal VirtualBox lab
- Host: server01
- Operating system: CentOS Stream 10
- Service: Apache HTTPD
- Monitoring and ticketing: Zabbix and Zammad

## Problem and Impact

During a simulated incident, Apache HTTPD failed to start. The web service hosted on the lab server was unavailable.

## Investigation

I checked the service state and reviewed its logs:

```bash
systemctl status httpd
journalctl -xeu httpd
```

I then validated the Apache configuration:

```bash
apachectl configtest
```

The configuration test identified a syntax error involving `INVALID_PORT` in the Apache configuration.

## Root Cause

The Listen directive contained an invalid port value:

```apache
Listen INVALID_PORT
```

This configuration error prevented Apache from starting.

## Resolution

I replaced the invalid directive with:

```apache
Listen 80
```

I validated the configuration before restarting the service:

```bash
apachectl configtest
systemctl restart httpd
```

The configuration test returned `Syntax OK`.

## Verification

I checked the service and tested its local HTTP response:

```bash
systemctl status httpd
curl -I http://localhost
```

Apache restarted successfully, and the local HTTP check confirmed that the service responded.

For network access, I also allowed TCP port 80 through the lab firewall:

```bash
firewall-cmd --permanent --add-port=80/tcp
firewall-cmd --reload
```

The firewall configuration supported remote access; it was separate from the syntax error that caused the startup failure.

## Monitoring Verification

Service recovery was checked through the lab monitoring and ticketing workflow using Zabbix and Zammad.

## Lessons Learned

- Service logs and configuration validation help identify startup failures.
- Validate Apache configuration before restarting the service.
- Check service health, HTTP responses, and monitoring after applying a fix.
