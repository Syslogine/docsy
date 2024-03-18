---
title: "Secure FiveM Server Database"
description: "Implement robust security measures to protect your FiveM server's database from potential attacks and unauthorized access."
weight: 0
---

## User Account Management

### Principle of Least Privilege

```sql
-- Create roles for FiveM server operations
CREATE ROLE fivem_read_only, fivem_data_entry, fivem_manager;

-- Grant minimum required permissions to each role
GRANT SELECT ON fivem.* TO fivem_read_only;
GRANT INSERT ON fivem.player_data TO fivem_data_entry;
GRANT INSERT, UPDATE, DELETE ON fivem.* TO fivem_manager;

-- Create users and assign roles
CREATE USER 'fivem_viewer'@'localhost' IDENTIFIED BY 'StrongPassword123!';
GRANT fivem_read_only TO 'fivem_viewer'@'localhost';

CREATE USER 'fivem_entry'@'localhost' IDENTIFIED BY 'AnotherStrongPass!';
GRANT fivem_data_entry TO 'fivem_entry'@'localhost';

CREATE USER 'fivem_admin'@'localhost' IDENTIFIED BY 'SuperSecurePass123!';
GRANT fivem_manager TO 'fivem_admin'@'localhost';
```

### Strong Password Policies

```sql
-- Enforce a strong password policy
SET GLOBAL validate_password.length=14;
SET GLOBAL validate_password.number_count=2;
SET GLOBAL validate_password.mixed_case_count=1;
SET GLOBAL validate_password.special_char_count=1;
SET GLOBAL validate_password.dictionary_file='/usr/share/mysql/english_dictionary.txt';

-- Update user password to comply with the new policy
ALTER USER 'fivem_viewer'@'localhost' IDENTIFIED BY 'N3wStr0ngPa$$word';
```

### Multi-Factor Authentication (MFA)

```sql
-- Install the MFA plugin
INSTALL PLUGIN authentication_mfa SONAME 'authentication_mfa.so';

-- Create an MFA-enabled user account
CREATE USER 'fivem_superadmin'@'localhost' IDENTIFIED BY 'UltraSecurePass123!';

-- Configure MFA for the user, using a hardware security key
ALTER USER 'fivem_superadmin'@'localhost'
IDENTIFIED WITH authentication_mfa
BY 'initial_secret_key'
REQUIRE SECURE_REMOTE_USER;
```

## Database Permissions

### Role-Based Access Control (RBAC)

```sql
-- Create a role for FiveM server developers
CREATE ROLE fivem_developer;
GRANT SELECT, INSERT, UPDATE ON fivem.resources TO fivem_developer;

-- Assign the role to a user
GRANT fivem_developer TO 'dev_user'@'%';
```

### Granular Permissions

```sql
-- Grant SELECT permission on specific tables
GRANT SELECT ON fivem.player_data, fivem.server_logs TO 'fivem_viewer'@'%';

-- Grant INSERT permission on specific columns
GRANT INSERT(name, score) ON fivem.player_scores TO 'fivem_entry'@'%';
```

### Secure Database Objects

```sql
-- Create a stored procedure for inserting player scores
DELIMITER $$
CREATE PROCEDURE InsertPlayerScore(
    IN p_name VARCHAR(50),
    IN p_score INT
)
BEGIN
    -- Input validation
    IF p_score < 0 THEN
        SIGNAL SQLSTATE '45000'
            SET MESSAGE_TEXT = 'Score cannot be negative';
    END IF;

    -- Check if player exists
    IF NOT EXISTS (SELECT 1 FROM player_data WHERE name = p_name) THEN
        SIGNAL SQLSTATE '45000'
            SET MESSAGE_TEXT = 'Player does not exist';
    END IF;

    -- Insert score
    INSERT INTO player_scores (name, score)
    VALUES (p_name, p_score);
END$$
DELIMITER ;

-- Grant execute permission on the stored procedure
GRANT EXECUTE ON PROCEDURE InsertPlayerScore TO 'fivem_entry'@'%';
```

```sql
-- Create a view that masks sensitive player data
CREATE VIEW player_data_public AS
SELECT name, game_id, join_date
FROM player_data;

-- Grant SELECT permission on the view
GRANT SELECT ON player_data_public TO 'fivem_viewer'@'%';
```