# GitLab CI – TCP Connectivity Check (Ansible)

## Overview

This GitLab CI pipeline performs **automated TCP connectivity checks** using Ansible.  
It is used to verify network access from infrastructure or Kubernetes nodes to external
services **before application deployment**.

The pipeline runs inside a **custom Ansible Docker image** and reads its targets from a
simple JSON configuration file.

---

## How It Works

1. Pipeline runs **only on the `main` branch**
2. GitLab Runner starts an Ansible Docker image
3. Target hosts and ports are read from `config.json`
4. Ansible checks TCP connectivity for each target
5. Results are collected in **JUnit format**
6. Pipeline fails if any TCP check fails

---

## Pipeline Rules

- Pipeline is skipped if only `README.md` is changed
- Pipeline runs only on the `main` branch
- All other cases are ignored

---

## Configuration

### `config.json`

Developers only need to edit this file:

```json
{
  "targets": [
    { "host": "10.10.10.20", "port": 5432 },
    { "host": "api.internal.local", "port": 443 }
  ]
}

