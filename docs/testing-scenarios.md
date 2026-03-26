# Testing Scenarios

This document outlines the key test cases performed to validate the Active-Active Multi-Context Failover deployment.

## 1. Normal Operation Verification

- Check both ASAs are operational
- Verify TCS Context is active on preferred ASA
- Verify Wipro Context is active on preferred ASA
- Confirm internet reachability from both TCS and Wipro internal networks
- Validate separate NAT translations for each context
- Check no cross-communication exists between TCS and Wipro networks

**Commands:**
```cisco
show failover
show context
show nat detail
show xlate
ping <internet-ip> source inside
2. Failover Testing

Shut down one physical ASA (simulate hardware failure)
Verify affected context automatically fails over to the secondary ASA
Confirm traffic continues without interruption from both companies
Validate sub-second or minimal disruption during failover
Check configuration synchronization after recovery

Commands:
ciscoshow failover
show failover state
3. Traffic Isolation Testing

Attempt communication from TCS network to Wipro network (should fail)
Confirm each context has its own independent routing table and security policies

4. Management Access Testing

Telnet/SSH from TCS internal router to ISP gateway
Telnet/SSH from Wipro internal router to ISP gateway
Verify access-list enforcement

5. Recovery Testing

Power on the failed ASA
Verify preempt brings contexts back to preferred ASA (if configured)
Confirm full redundancy is restored


Note: All tests were performed in EVE-NG lab environment. Proper documentation and screenshots of test results are available in the screenshots/ folder.