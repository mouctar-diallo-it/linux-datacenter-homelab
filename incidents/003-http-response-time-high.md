
# Incident 003 — HTTP Response Time Too High

## Issue

Zabbix detected abnormally high HTTP response time on `server01`.

- Host: `server01.dclab.local`
- Severity: Average
- Zabbix Problem ID: 2865
- Zammad Ticket ID: 101

## Detection

Zabbix Web Monitoring generated the following alert:

`HTTP response time is too high on server01`

The configured trigger detected an HTTP response time greater than 2 seconds.

Zammad automatically generated a ticket for the incident.

## Investigation

HTTP connectivity was first tested from the Zabbix server:

```bash
curl -o /dev/null -s -w 'HTTP: %{http_code}\nTotal time: %{time_total}s\n' http://10.10.10.10
