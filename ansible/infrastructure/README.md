# README 1: TCP Connection Check (Ansible)



# TCP Connection Check – Ansible

## Overview

This project provides an **Ansible-based TCP connectivity check** that verifies network access from infrastructure nodes to external systems and subsystems.

---

## Use Case

In many enterprise environments, applications depend on multiple external services such as:

* Databases (MySQL, PostgreSQL, Oracle)
* Internal APIs
* Message brokers
* Legacy systems

This project helps answer a simple but critical question:

> *Can this node reach the required destination and port?*

---

## How It Works

1. Target nodes are defined in `inventory/hosts.ini`
2. Destinations and ports are defined as variables (or external JSON in CI)
3. The playbook runs TCP checks from each node

---

## Inventory Example

```ini
[k8s_nodes]
node1 ansible_host=192.168.10.21
node2 ansible_host=192.168.10.22
```

---


## Output

* ok: [192.168.0.101] => {
    "msg": "Source-IP: 192.168.0.101 Destination-IP: 192.168.0.123  port 80  Status: Connection refused! ❕❕❕"

* ok: [192.168.0.103] => {
    "msg": "Source-IP: 192.168.0.103 Destination-IP: 192.168.0.124  port 22  Status: succeeded ✔️✔️✔️" }

* ok: [192.168.0.103] => {
    "msg": "Source-IP: 192.168.0.103 Destination-IP: 192.168.0.125  port 25  Status: No route to host! ❕❕❕" }

---

## Typical Usage Scenarios

* Pre-deployment network validation
* Kubernetes node connectivity checks
* Troubleshooting firewall or routing issues

---


## Notes

* No application code changes required
* No direct server access for developers
* Can be extended for UDP or TLS checks

---
