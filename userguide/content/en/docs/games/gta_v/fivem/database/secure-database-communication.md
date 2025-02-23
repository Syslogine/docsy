---
title: "Secure Database Communication"
description: "Implement secure communication channels between game servers and the database using encryption, certificate-based authentication, IP restrictions, and role-based access control."
weight: 2
---

## Use Encrypted Connections (SSL/TLS)

```sql
-- MySQL: Enable SSL/TLS for database connections
# 1. Generate SSL certificates
openssl genrsa 2048 > ca-key.pem
openssl req -new -x509 -nodes -days 3600 -key ca-key.pem -out ca.pem
openssl req -newkey rsa:2048 -days 3600 -nodes -keyout server-key.pem -out server-req.pem
openssl rsa -in server-key.pem -out server-key.pem
openssl x509 -req -in server-req.pem -days 3600 -CA ca.pem -CAkey ca-key.pem -set_serial 01 -out server-cert.pem

# 2. Configure MySQL to use SSL
[mysqld]
ssl-ca=ca.pem
ssl-cert=server-cert.pem
ssl-key=server-key.pem

# 3. Connect using SSL
mysql --ssl-ca=ca.pem --ssl-cert=client-cert.pem --ssl-key=client-key.pem
```

```sql
-- PostgreSQL: Enable SSL/TLS for database connections
# 1. Generate SSL certificates
openssl req -new -text -out server.req
openssl rsa -in privkey.pem -modulus -noout -out modulus
openssl req -x509 -in server.req -text -key privkey.pem -out server.crt
chmod og-rwx privkey.pem

# 2. Configure PostgreSQL to use SSL
ssl = on
ssl_cert_file = 'server.crt'
ssl_key_file = 'privkey.pem'

# 3. Connect using SSL
psql "host=localhost user=postgres sslmode=require"
```

## Enforce Certificate-Based Authentication

```sql
-- MySQL: Configure certificate-based authentication
# 1. Generate client certificates
openssl req -newkey rsa:2048 -days 3600 -nodes -keyout client-key.pem -out client-req.pem
openssl rsa -in client-key.pem -out client-key.pem
openssl x509 -req -in client-req.pem -days 3600 -CA ca.pem -CAkey ca-key.pem -set_serial 01 -out client-cert.pem

# 2. Configure MySQL to use certificate-based authentication
[mysqld]
ssl-ca=ca.pem
ssl-cert=server-cert.pem
ssl-key=server-key.pem

[client]
ssl-ca=ca.pem
ssl-cert=client-cert.pem
ssl-key=client-key.pem
```

```sql
-- PostgreSQL: Configure certificate-based authentication
# 1. Generate client certificates
openssl req -new -text -out client.req
openssl rsa -in privkey.pem -modulus -noout -out modulus
openssl req -x509 -in client.req -text -key privkey.pem -out client.crt

# 2. Configure PostgreSQL to use certificate-based authentication
hostssl all all 0.0.0.0/0 cert clientcert=1
```

## Restrict Database Access to Specific IP Addresses/Networks

```sql
-- MySQL: Restrict access to specific IP addresses/networks
CREATE USER 'game_server'@'192.168.1.100' IDENTIFIED BY 'StrongPassword123!';
GRANT ALL PRIVILEGES ON fivem.* TO 'game_server'@'192.168.1.100';
```

```
-- PostgreSQL: Restrict access to specific IP addresses/networks (pg_hba.conf)
host    fivem             game_server        192.168.1.100/32         md5
```

## Implement Database User Roles and Permissions

```sql
-- MySQL: Create roles and assign permissions
CREATE ROLE fivem_read_only, fivem_data_entry, fivem_manager;

GRANT SELECT ON fivem.* TO fivem_read_only;
GRANT INSERT ON fivem.player_data TO fivem_data_entry;
GRANT INSERT, UPDATE, DELETE ON fivem.* TO fivem_manager;

CREATE USER 'game_viewer'@'192.168.1.100' IDENTIFIED BY 'StrongPassword123!';
GRANT fivem_read_only TO 'game_viewer'@'192.168.1.100';
```

```sql
-- PostgreSQL: Create roles and assign permissions
CREATE ROLE fivem_read_only;
GRANT SELECT ON ALL TABLES IN SCHEMA fivem TO fivem_read_only;

CREATE ROLE fivem_data_entry;
GRANT INSERT ON fivem.player_data TO fivem_data_entry;

CREATE ROLE fivem_manager;
GRANT INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA fivem TO fivem_manager;

CREATE USER game_viewer WITH PASSWORD 'StrongPassword123!';
GRANT fivem_read_only TO game_viewer;
```
