# SSH Failed Authentication Investigation

## Overview

This lab documents the investigation of a failed SSH authentication attempt detected on my Ubuntu SOC homelab.

The objective was to practice a basic SOC L1 triage workflow by identifying the source of the authentication attempt, determining whether the activity was repeated, and verifying whether any successful authentication occurred.

## Environment

* Host: `UBUNTU-SOC`
* Operating System: Ubuntu Linux
* Service: OpenSSH
* Protocol: SSH
* Destination Port: TCP/22
* Environment: Local cybersecurity homelab

## Initial Event

A failed SSH authentication attempt was identified for a non-existent account.

Observed indicators:

* Username: `falseuser`
* Source IP: `127.0.0.1`
* Authentication result: Failed
* User status: Invalid user
* Protocol: SSH

Example log:

```text
Failed password for invalid user falseuser from 127.0.0.1 port [ephemeral-port] ssh2
```

## Investigation

### 1. Source Analysis

The source IP was identified as:

`127.0.0.1`

This address belongs to the IPv4 loopback range, indicating that the authentication attempt originated from the local host rather than an external system.

### 2. Authentication Failure Analysis

The SSH logs showed an authentication failure associated with an invalid username.

The account `falseuser` did not exist on the system.

At this stage, the event alone was not considered sufficient evidence of malicious activity.

### 3. Frequency Analysis

SSH authentication logs from the surrounding 30-minute window were reviewed to determine whether the event was part of repeated authentication attempts.

Only one failed authentication event was identified.

No pattern consistent with brute-force activity was observed.

### 4. Successful Authentication Check

The SSH logs were searched for successful authentication events using the `Accepted` indicator.

No successful SSH authentication events were identified during the investigated time window.

## Assessment

Based on the available evidence:

* Only one failed authentication attempt occurred.
* The attempted username was invalid.
* The source was the local host (`127.0.0.1`).
* No repeated authentication attempts were identified.
* No successful SSH authentication followed the event.
* No additional suspicious activity was observed.

## Disposition

**Severity:** Informational / Low

**Classification:** Benign lab activity

**Escalation:** Not required

The event was documented for training purposes and as a baseline for future correlation with more complex authentication scenarios.

## What I Learned

This investigation demonstrated that a failed authentication event should not automatically be treated as a security incident.

Context and correlation are necessary before escalation.

The investigation included:

* Identifying the source IP
* Understanding loopback addressing
* Identifying invalid-user authentication
* Reviewing authentication frequency
* Searching for successful authentication
* Establishing an investigation time window
* Making an evidence-based escalation decision

## Next Step

The next lab will expand this scenario by generating multiple failed SSH authentication attempts and introducing additional activity to determine when an authentication alert should be escalated.
