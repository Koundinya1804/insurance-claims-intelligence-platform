\# Insurance Claims Intelligence Platform

\# Canonical Domain Model



\## Purpose



This document defines the canonical insurance-domain entities used across

the entire application.



This is a shared contract between the Guidewire/Insurance Domain layer,

Cloud/Data Engineering layer, Backend layer, ML layer, and Analytics layer.



Any change to these definitions must be reviewed before implementation.



\---



\## 1. Customer



Represents the insured/customer associated with one or more insurance policies.



\### Core attributes



\- customer\_id

\- first\_name

\- last\_name

\- date\_of\_birth

\- customer\_type

\- region

\- created\_at

\- updated\_at



\### Relationships



Customer 1 ─── N Policy



Customer 1 ─── N Claim



\---



\## 2. Policy



Represents an insurance policy/contract associated with a customer.



\### Core attributes



\- policy\_id

\- policy\_number

\- customer\_id

\- policy\_type\_id

\- status

\- start\_date

\- end\_date

\- premium\_amount

\- created\_at

\- updated\_at



\### Relationships



Policy N ─── 1 Customer



Policy N ─── 1 PolicyType



Policy 1 ─── N PolicyCoverage



Policy 1 ─── N Claim



\---



\## 3. PolicyType



Defines the category/type of insurance policy.



Examples may include:



\- Auto

\- Health

\- Property

\- Travel



The initial implementation will use a controlled set of synthetic policy types.



\---



\## 4. PolicyCoverage



Represents a specific coverage associated with a policy.



\### Core attributes



\- coverage\_id

\- policy\_id

\- coverage\_type

\- coverage\_limit

\- deductible

\- premium\_component



\### Relationship



Policy 1 ─── N PolicyCoverage



\---



\## 5. Claim



Represents a claim filed against an insurance policy.



\### Core attributes



\- claim\_id

\- policy\_id

\- customer\_id

\- claim\_type

\- status

\- claim\_amount

\- claim\_date

\- settlement\_date

\- location

\- description

\- created\_at

\- updated\_at



\### Relationships



Claim N ─── 1 Policy



Claim N ─── 1 Customer



Claim 1 ─── N ClaimEvent



Claim 1 ─── N RiskScore



\---



\## 6. ClaimEvent



Represents an event in the lifecycle of a claim.



\### Core attributes



\- event\_id

\- claim\_id

\- event\_type

\- previous\_status

\- new\_status

\- event\_timestamp

\- performed\_by

\- notes



\### Relationship



Claim 1 ─── N ClaimEvent



Claim events provide an auditable history of claim state transitions.



\---



\## 7. RiskScore



Represents an ML-generated claim risk assessment.



\### Core attributes



\- risk\_score\_id

\- claim\_id

\- model\_version

\- risk\_score

\- risk\_level

\- reason\_codes

\- prediction\_timestamp



\### Risk score



Range:



0–100



\### Risk levels



\- 0–30: LOW

\- 31–70: MEDIUM

\- 71–100: HIGH



These thresholds are application-level business definitions and may be

revisited after model evaluation.



\### Relationship



Claim 1 ─── N RiskScore



Multiple scores may exist for a claim because different model versions

or prediction timestamps may produce different assessments.



\---



\## 8. User



Represents an authenticated application user.



\### Core attributes



\- user\_id

\- username

\- password\_hash

\- role\_id

\- is\_active

\- created\_at



\---



\## 9. Role



Defines application permissions.



Initial roles:



\- ADMIN

\- CLAIMS\_ANALYST

\- MANAGER



\---



\# Entity Relationship Summary



Customer

&#x20;   |

&#x20;   | 1:N

&#x20;   v

Policy

&#x20;   |

&#x20;   +--------> PolicyCoverage

&#x20;   |

&#x20;   | 1:N

&#x20;   v

Claim

&#x20;   |

&#x20;   +--------> ClaimEvent

&#x20;   |

&#x20;   +--------> RiskScore



Policy

&#x20;   |

&#x20;   +--------> PolicyType



User

&#x20;   |

&#x20;   +--------> Role



\---



\# Guidewire Relationship



These entities represent our synthetic insurance-domain model.



They are conceptually aligned with insurance concepts commonly handled

within Guidewire InsuranceSuite.



This project does NOT currently claim direct integration with Guidewire.



If a licensed/authorized Guidewire environment becomes available,

integration will be introduced through a defined integration boundary

rather than by directly coupling the application to Guidewire internals.



\---



\# Change Management



Changes to canonical entities must consider:



1\. Database schema

2\. Data pipeline

3\. API contracts

4\. ML features

5\. Analytics

6\. Guidewire domain documentation



A shared interface must not be changed silently.

