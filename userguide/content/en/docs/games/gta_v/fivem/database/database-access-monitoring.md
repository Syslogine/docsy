---
title: "Database Access Monitoring"
description: "Monitor database activities, implement intrusion detection/prevention systems, set up alerts for potential threats, and regularly review logs to ensure the security of your database."
weight: 4
---

## Enable Database Activity Logging

```sql
-- MySQL: Enable and configure audit logging
INSTALL SONAME 'server_audit';
SET GLOBAL server_audit_logging=ON;
SET GLOBAL server_audit_file_rotate_size=1000000; # Rotate log files at 1MB
SET GLOBAL server_audit_file_rotate_max_retained_files=10; # Keep 10 log files

-- Configure log events to capture
SET GLOBAL server_audit_events='CONNECT,QUERY';
```

```sql
-- PostgreSQL: Enable and configure logging
# Edit the postgresql.conf file
log_destination = 'csvlog'
logging_collector = on
log_directory = 'pg_log'
log_filename = 'postgresql-%Y-%m-%d_%H%M%S.log'
log_truncate_on_rotation = off
log_rotation_age = 1d
log_rotation_size = 100000 # Rotate log files at 100MB
```

## Implement Intrusion Detection/Prevention Systems (IDS/IPS)

```bash
# Install and configure an IDS/IPS solution like Snort or Suricata
# Example for Snort on Ubuntu
sudo apt-get install snort

# Configure Snort to monitor database traffic
# Edit the snort.conf file
ipvar HOME_NET 192.168.1.0/24
ipvar EXTERNAL_NET !$HOME_NET

# Add rules to detect potential threats
include $RULE_PATH/mysql.rules
include $RULE_PATH/postgresql.rules
include $RULE_PATH/sql-injection.rules

# Start Snort in IDS mode
sudo snort -A console -q -u snort -g snort -c /etc/snort/snort.conf -i eth0
```

## Set up Alerts for Potential Threats

```sql
-- MySQL: Set up alerts for failed login attempts and SQL injection
DELIMITER $$
CREATE TRIGGER failed_login_attempts_trigger
AFTER INSERT ON mysql.general_log
FOR EACH ROW
BEGIN
    IF NEW.argument LIKE 'ACCESS DENIED%' THEN
        INSERT INTO failed_login_attempts (user, host, timestamp)
        VALUES (SUBSTRING_INDEX(NEW.argument, '@', 1),
                SUBSTRING_INDEX(SUBSTRING_INDEX(NEW.argument, '@', -1), ']', 1),
                NEW.event_time);
    END IF;
END$$
DELIMITER ;

DELIMITER $$
CREATE TRIGGER sql_injection_attempts_trigger
AFTER INSERT ON mysql.general_log
FOR EACH ROW
BEGIN
    IF NEW.argument RLIKE '(^(\\\\\\\'|\\\'|\\%27|\')|\\b(union|select|insert|update|delete)\\b.*(\\b(from|into)\\b.*(\\b(information_schema|mysql|sys|data)\\b|\\bconcaten\\(|\\bchar\\())|\\b(outfile|load_file|into|dumpfile))' THEN
        INSERT INTO sql_injection_attempts (user, host, query, timestamp)
        VALUES (SUBSTRING_INDEX(NEW.argument, '@', 1),
                SUBSTRING_INDEX(SUBSTRING_INDEX(NEW.argument, '@', -1), ']', 1),
                NEW.argument,
                NEW.event_time);
    END IF;
END$$
DELIMITER ;
```

```sql
-- PostgreSQL: Set up alerts for failed login attempts and SQL injection
CREATE EXTENSION IF NOT EXISTS log_fdw;

CREATE SERVER log_server
FOREIGN DATA WRAPPER log_fdw
OPTIONS (filename '/var/log/postgresql/postgresql-%Y-%m-%d_%H%M%S.log');

CREATE TABLE failed_login_attempts (
    username TEXT,
    client_addr TEXT,
    timestamp TIMESTAMP
);

CREATE RULE failed_login_alert AS
ON INSERT TO failed_login_attempts
WHERE NEW.username IS NOT NULL
DO NOTIFY failed_login_attempt,
           E'Username: ' || NEW.username || E'\nClient Address: ' || NEW.client_addr || E'\nTimestamp: ' || NEW.timestamp;

CREATE VIEW failed_logins WITH (security_barrier) AS
SELECT
    split_part(message, ' ', 10) AS username,
    split_part(message, ' ', 11) AS client_addr,
    timestamp
FROM pg_log.postgresql_log
WHERE message LIKE 'FATAL%password authentication failed for user%';
```

## Regularly Review and Analyze Logs

```bash
# Analyze MySQL audit logs
sudo mysqlauditgrep --query-log=/var/log/mysql/audit.log --query-pam-ksok --query-has-comment-augment --query-has-sleep-augment --query-has-delay-augment

# Analyze PostgreSQL logs
sudo grep 'FATAL' /var/log/postgresql/*.log | awk '{print $1, $2, $3, $4, $5, $6, $7, $8, $9, $10, $11}'
```
