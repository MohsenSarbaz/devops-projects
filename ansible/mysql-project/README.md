# MySQL Installation and User Management (Ansible)


# MySQL Automation – Installation & User Management

## Overview

This Ansible project automates:

* Installation of MySQL Server
* Secure initial configuration
* Database creation
* User creation
* Permission and access management

It is designed for **repeatable, idempotent, and secure** MySQL provisioning in infrastructure environments.

---

## Use Case

This project is useful when:

* Provisioning MySQL for applications
* Standardizing database setup across environments
* Automating user and permission management
* Eliminating manual database configuration

---

## Features

* Installs MySQL using system package manager
* Ensures MySQL service is running and enabled
* Creates databases
* Creates users with defined privileges
* Supports multiple users and databases via variables

---

## Inventory Example

```ini
[mysql_servers]
db01 ansible_host=192.168.20.10
```

---

## Security Considerations

* Passwords should be stored using **Ansible Vault** in production
* Remote root login should be disabled
* Firewall rules should restrict MySQL access

---

## Typical Usage Scenarios

* Application database provisioning
* CI/CD environment setup
* Development and staging environments
* Infrastructure-as-Code database management
