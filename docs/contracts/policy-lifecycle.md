\# Policy Lifecycle Contract



\## Canonical Policy States



Initial states:



1\. DRAFT

2\. QUOTED

3\. BOUND

4\. ACTIVE

5\. RENEWAL\_PENDING

6\. RENEWED

7\. CANCELLED

8\. EXPIRED



\---



\## Valid Transitions



DRAFT

&#x20; ↓

QUOTED



QUOTED

&#x20; ↓

BOUND



BOUND

&#x20; ↓

ACTIVE



ACTIVE

&#x20; ├──→ RENEWAL\_PENDING

&#x20; └──→ CANCELLED



RENEWAL\_PENDING

&#x20; ├──→ RENEWED

&#x20; └──→ EXPIRED



RENEWED

&#x20; ↓

ACTIVE



\---



\## Business Rules



1\. A policy must have a valid customer.

2\. A policy must have a valid policy type.

3\. End date must not precede start date.

4\. Premium amount cannot be negative.

5\. A cancelled policy cannot be treated as active.

6\. An expired policy cannot be renewed without an applicable renewal

&#x20;  workflow.

7\. State transitions must be recorded where auditability is required.



\---



\## Guidewire Domain Mapping



These states represent a conceptual insurance policy lifecycle.



They are not claimed to be exact Guidewire PolicyCenter internal

configuration or state values.

