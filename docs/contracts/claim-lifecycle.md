\# Claim Lifecycle Contract



\## Purpose



Defines the canonical claim lifecycle used throughout the Insurance Claims

Intelligence \& Automation Platform.



This is a shared contract between the insurance domain, database,

backend, data pipeline, workflow, ML, and analytics layers.



\---



\## Claim States



The initial canonical states are:



1\. FILED

2\. UNDER\_REVIEW

3\. INVESTIGATION

4\. APPROVED

5\. REJECTED

6\. SETTLED



\---



\## Valid Transitions



FILED

&#x20; ↓

UNDER\_REVIEW



UNDER\_REVIEW

&#x20; ↓

INVESTIGATION



INVESTIGATION

&#x20; ├──→ APPROVED

&#x20; └──→ REJECTED



APPROVED

&#x20; ↓

SETTLED



\---



\## Transition Rules



\### FILED → UNDER\_REVIEW



A newly submitted claim can enter review.



\### UNDER\_REVIEW → INVESTIGATION



A claim requiring additional investigation may move into investigation.



\### INVESTIGATION → APPROVED



A claim that satisfies the applicable business validation may be approved.



\### INVESTIGATION → REJECTED



A claim that fails applicable business rules may be rejected.



\### APPROVED → SETTLED



An approved claim may proceed to settlement.



\---



\## Invalid Transitions



The application must reject invalid state transitions.



Examples:



\- FILED → SETTLED

\- FILED → APPROVED

\- REJECTED → SETTLED

\- SETTLED → INVESTIGATION



unless a future business requirement explicitly introduces a valid

transition.



\---



\## Auditability



Every valid status transition should create a ClaimEvent.



Example:



Claim CL1001:



FILED

→ UNDER\_REVIEW

→ INVESTIGATION

→ APPROVED

→ SETTLED



The event history should preserve:



\- previous status

\- new status

\- timestamp

\- actor

\- notes where applicable



\---



\## Guidewire Domain Mapping



This lifecycle is a synthetic application-level representation of

insurance claims processing concepts.



It must not be presented as an exact copy of Guidewire ClaimCenter's

internal workflow configuration.



If a real Guidewire environment becomes available, the actual workflow

configuration must be verified before claiming compatibility.

