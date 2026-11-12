
## Evidence

### 1. Monitoring Alert

Zabbix/Zammad detected that the HTTP application on `server01` was unavailable.

![HTTP application unavailable alert](screenshots/incident-007/01-http-application-unavailable-alert.png)

### 2. HTTPD Service Failure

The Apache service was checked and found in a failed state.

![HTTPD service failed](screenshots/incident-007/02-httpd-service-failed.png)

### 3. Configuration Syntax Error

`apachectl configtest` identified an invalid directive on line 357 of `/etc/httpd/conf/httpd.conf`.

![Apache configuration syntax error](screenshots/incident-007/03-apache-configuration-syntax-error.png)

### 4. Configuration Corrected

After removing the invalid directive, the Apache configuration test returned `Syntax OK`.

![Apache configuration corrected](screenshots/incident-007/04-apache-configuration-corrected.png)

### 5. HTTP Service Restored

Apache returned to an active state and the application responded with `HTTP/1.1 200 OK`.

![HTTP service restored](screenshots/incident-007/05-http-service-restored.png)

### 6. Monitoring Recovery

Zabbix/Zammad confirmed that the incident was automatically resolved.

![Monitoring recovery](screenshots/incident-007/06-monitoring-recovery.png)
