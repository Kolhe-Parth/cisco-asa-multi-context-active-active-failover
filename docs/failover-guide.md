# ASA Active-Active Failover Configuration Guide

This document provides a high-level overview of the Active-Active Failover setup used in this Multi-Context project.

## Overview

In Active-Active Failover with Multi-Context, both physical ASA firewalls actively handle traffic simultaneously. This is achieved using **Failover Groups**.

- Failover Group 1 → Can be active on ASA1 (TCS Context preferred)
- Failover Group 2 → Can be active on ASA2 (Wipro Context preferred)

This design provides load sharing along with redundancy.

## Key Commands (Executed in System Context)

```cisco
! Enable Failover
failover

! Configure Failover Link
failover lan unit primary
failover lan interface FAILOVER Ethernet4
failover link FAILOVER Ethernet4

! Failover Group Configuration
failover group 1
 primary
 preempt
 replicate http

failover group 2
 secondary
 preempt
 replicate http
Important Notes

Each context must be assigned to a specific failover group.
Configuration and state information are synchronized between the two ASAs.
When one ASA fails, the affected context automatically becomes active on the surviving ASA.
Preempt ensures the preferred ASA regains active role after recovery.

Best Practices

Use a dedicated interface for the failover link (recommended).
Ensure failover link has sufficient bandwidth and low latency.
Test failover thoroughly in a lab environment before production deployment.
Monitor failover status regularly using show failover command.

For detailed configuration steps, refer to the official Cisco ASA Configuration Guide for Version 9.1.
