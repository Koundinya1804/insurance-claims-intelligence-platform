\# Insurance Claims Intelligence Platform



\# Data Dictionary



\*\*Owner:\*\* Koundinya  

\*\*Phase:\*\* 3 — Synthetic Data \& Database Schema  

\*\*Version:\*\* 1.0



\---



\# 1. Purpose



This document defines the business meaning of the core insurance

entities and their attributes.



It provides the business/domain reference for the PostgreSQL

implementation.



The technical database implementation must preserve the semantics

defined here.



\---



\# 2. Customer



Represents the insurance customer associated with one or more policies.



| Field | Type | Required | Description |

|---|---|---|---|

| customer\_id | UUID/String | Yes | Unique customer identifier |

| customer\_number | String | Yes | Business identifier |

| first\_name | String | Yes | Synthetic first name |

| last\_name | String | Yes | Synthetic last name |

| date\_of\_birth | Date | Yes | Synthetic date of birth |

| email | String | Yes | Synthetic email |

| phone | String | No | Synthetic phone number |

| region | String | Yes | Customer geographic region |

| created\_at | Timestamp | Yes | Record creation timestamp |



All customer information must be synthetic.



\---



\# 3. Policy



Represents an insurance policy associated with a customer.



| Field | Type | Required | Description |

|---|---|---|---|

| policy\_id | UUID/String | Yes | Unique policy identifier |

| policy\_number | String | Yes | Business policy identifier |

| customer\_id | UUID/String | Yes | Owning customer |

| policy\_type\_id | UUID/String | Yes | Policy type |

| status | Enum | Yes | Policy lifecycle status |

| start\_date | Date | Yes | Policy effective date |

| end\_date | Date | Yes | Policy expiration date |

| premium\_amount | Decimal | Yes | Policy premium |

| created\_at | Timestamp | Yes | Record creation timestamp |



\---



\# 4. Policy Type



Represents the category of insurance policy.



Initial synthetic policy types may include:



\- Auto

\- Home

\- Health

\- Travel

\- Property



The final dataset should use only policy types supported by the

implemented domain model.



\---



\# 5. Policy Coverage



Represents coverage associated with a policy.



| Field | Type | Required | Description |

|---|---|---|---|

| coverage\_id | UUID/String | Yes | Unique coverage identifier |

| policy\_id | UUID/String | Yes | Associated policy |

| coverage\_type | String | Yes | Coverage category |

| coverage\_limit | Decimal | Yes | Maximum covered amount |

| deductible | Decimal | Yes | Applicable deductible |

| premium\_component | Decimal | No | Premium attributable to coverage |



A policy may contain multiple coverage records.



\---



\# 6. Claim



Represents an insurance claim submitted against a policy.



| Field | Type | Required | Description |

|---|---|---|---|

| claim\_id | UUID/String | Yes | Unique claim identifier |

| claim\_number | String | Yes | Business claim identifier |

| policy\_id | UUID/String | Yes | Referenced policy |

| customer\_id | UUID/String | Yes | Claim customer |

| claim\_type | String | Yes | Type of claim |

| status | Enum | Yes | Claim lifecycle status |

| claim\_amount | Decimal | Yes | Requested claim amount |

| claim\_date | Date | Yes | Date claim was filed |

| settlement\_date | Date | No | Settlement date |

| description | Text | Yes | Synthetic claim description |

| location | String | Yes | Claim location |

| created\_at | Timestamp | Yes | Record creation timestamp |



\---



\# 7. Claim Event



Represents a state transition or significant claim workflow event.



| Field | Type | Required | Description |

|---|---|---|---|

| event\_id | UUID/String | Yes | Unique event identifier |

| claim\_id | UUID/String | Yes | Associated claim |

| previous\_status | Enum | No | Previous claim state |

| new\_status | Enum | Yes | New claim state |

| event\_timestamp | Timestamp | Yes | Event timestamp |

| performed\_by | UUID/String | No | Acting user |

| notes | Text | No | Synthetic event notes |



\---



\# 8. Risk Score



Represents an ML-generated claim risk assessment.



| Field | Type | Required | Description |

|---|---|---|---|

| risk\_score\_id | UUID/String | Yes | Unique risk assessment |

| claim\_id | UUID/String | Yes | Associated claim |

| risk\_score | Decimal | Yes | Score from 0 to 100 |

| risk\_level | Enum | Yes | LOW/MEDIUM/HIGH |

| model\_version | String | Yes | Model version |

| explanation | JSON/Text | Yes | Explainability information |

| generated\_at | Timestamp | Yes | Prediction timestamp |



\---



\# 9. User



Represents an authenticated application user.



| Field | Type | Required | Description |

|---|---|---|---|

| user\_id | UUID/String | Yes | Unique user identifier |

| username | String | Yes | Login identifier |

| password\_hash | String | Yes | Hashed password |

| role\_id | UUID/String | Yes | Assigned role |

| active | Boolean | Yes | Account status |

| created\_at | Timestamp | Yes | Account creation timestamp |



Plain-text passwords must never be stored.



\---



\# 10. Role



Initial application roles:



\- ADMIN

\- CLAIMS\_ANALYST

\- MANAGER



Role permissions are defined by the application security model.



\---



\# 11. Relationships



```text

Customer

&#x20;  |

&#x20;  | 1:N

&#x20;  v

Policy

&#x20;  |

&#x20;  | 1:N

&#x20;  +------> PolicyCoverage

&#x20;  |

&#x20;  | 1:N

&#x20;  v

Claim

&#x20;  |

&#x20;  | 1:N

&#x20;  +------> ClaimEvent

&#x20;  |

&#x20;  | 1:N

&#x20;  v

RiskScore

