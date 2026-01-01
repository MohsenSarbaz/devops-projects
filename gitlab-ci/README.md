# GitLab CI – TCP Connectivity Check (Ansible)

## Overview

This project provides a GitLab CI pipeline that performs **TCP connectivity checks**
using Ansible that integrated with Gitlab.

It is mainly used to verify **network connectivity between servers and services**
before running or deploying applications.

This pipeline is very useful when a service needs to connect to **many different IP
addresses and ports**, (like databases, brokers, ...) and you want to validate all connections in one pipeline run.

The pipeline runs inside a **custom Ansible Docker image** and generates a
connectivity report as an artifact.

---

## How It Works

1. The pipeline is triggered manually from the GitLab UI or by a branch commit
2. The user must provide **USERNAME** and **PASSWORD** when running the pipeline
3. GitLab Runner starts the Ansible Docker image
4. Source hosts are read from `Source.ini`
5. Destination hosts and ports are read from `Destination.json`
6. Ansible checks TCP connectivity for each destination
7. Results are written to a CSV file with a timestamp
8. The CSV report is uploaded as a pipeline artifact

---

## Pipeline Rules

- Pipeline runs when triggered from the GitLab Web UI
- Pipeline runs for branch commits
- All other cases are ignored

---

## Required Variables

The following variables **must be provided** when running the pipeline:

| Variable | Description |
|--------|------------|
| `USERNAME` | SSH username used by Ansible |
| `PASSWORD` | SSH password used by Ansible |

If any of these variables are missing, the pipeline will stop immediately. And shows this massage :
`Please provide the USERNAME variable` or `Please provide the PASSWORD variable`

---

## Configuration

### `Source.ini`
This file defines the **source host(s)** where Ansible runs the connectivity checks from.
Example:
```ini
[source]
10.10.10.10
```
### `Destination.json`
This file defines the **destination IP addresses and ports** that should be checked
by the pipeline.
Each entry contains a destination host and a TCP port.
Example:
```json
{
  "targets": [
    { "host": "10.10.10.20", "port": 5432 },
    { "host": "api.internal.local", "port": 443 }
  ]
}
```

---
## **Connectivity Report**

At the end of the pipeline, a CSV file called tcp-report.csv is generated.
This file contains the result of each TCP connectivity check, including:
✔️Timestamp of the check
✔️Source host
✔️Destination host
✔️Destination port
✔️Connection status (which is `succeeded` or `Connection refused` or `Timeout or no response (Trying...)` )

---

## **Artifacts**

- Artifact name: `tcp-report.csv`
- Generated even if some checks fail
- Available for **1 hour**
This allows the user to easily review the results and visually check the  
connectivity status.

---
## **Use Case**

This pipeline is useful for:
- Checking network connectivity before deployments
- Verifying firewall or routing changes
- Troubleshooting service connection issues
- Environments with many service dependencies
---

## Feedback & Contact

If you have any ideas, suggestions, or if you notice any issues,
please feel free to reach out and connect with me.

I’m always open to feedback and improvements :)

