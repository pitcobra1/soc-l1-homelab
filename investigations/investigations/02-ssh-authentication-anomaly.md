# Lab 02 — SSH Authentication Anomaly

## Scenario

Multiple SSH authentication failures were observed on `UBUNTU-SOC`, involving different usernames and originating from `127.0.0.1`.

Unlike the previous lab, the failed attempts were followed by a **successful SSH authentication** to the valid account `socuser`.

## Investigation

SSH logs were reviewed and correlated within the alert timeframe.

The investigation identified:

* Multiple failed authentication attempts
* Attempts against invalid usernames
* A successful authentication to `socuser`
* Source IP: `127.0.0.1`
* Successful login at `10:29:10`

After confirming the successful authentication, the investigation pivoted to post-login activity.

No suspicious activity was identified in the available system journal.

## Key Finding

The investigation exposed a **telemetry gap**.

Although the successful SSH login could be confirmed, the available logs were not sufficient to reconstruct all activity performed during the authenticated session.

Therefore, absence of suspicious events in the journal could not be treated as proof that no post-login activity occurred.

## Assessment

**Result:** No confirmed compromise
**Containment:** Not required
**Escalation:** Not required in this lab scenario

The event was documented for future correlation.

## Next Step

Improve Linux auditing to provide visibility into process execution, privilege escalation, and post-authentication activity for the next investigation.
