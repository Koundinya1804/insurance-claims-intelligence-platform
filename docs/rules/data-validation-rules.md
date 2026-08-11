\# Insurance Claims Intelligence Platform



\# Data Validation Rules



\*\*Owner:\*\* Koundinya  

\*\*Implementation Owner:\*\* Saad



\---



\# 1. Purpose



Defines data-quality requirements for insurance data entering the

curated platform dataset.



\---



\# 2. Customer Validation



\- customer\_id must be present

\- customer\_number must be unique

\- required customer fields must be populated

\- date\_of\_birth must be a valid date



\---



\# 3. Policy Validation



\- policy\_id must be unique

\- policy\_number must be unique

\- customer\_id must reference an existing customer

\- policy\_type\_id must reference a valid policy type

\- start\_date must be valid

\- end\_date must be valid

\- end\_date must not precede start\_date

\- premium\_amount must not be negative

\- status must be a valid policy lifecycle state



\---



\# 4. Coverage Validation



\- coverage\_id must be unique

\- policy\_id must reference an existing policy

\- coverage\_limit must not be negative

\- deductible must not be negative



\---



\# 5. Claim Validation



\- claim\_id must be unique

\- claim\_number must be unique

\- policy\_id must reference an existing policy

\- customer\_id must reference an existing customer

\- claim customer must match policy customer

\- claim\_amount must not be negative

\- claim\_date must be valid

\- status must be a valid claim lifecycle state



\---



\# 6. Claim Event Validation



\- event\_id must be unique

\- claim\_id must reference an existing claim

\- new\_status must be valid

\- transition must be allowed by the claim lifecycle contract

\- event timestamp must be logically ordered



\---



\# 7. Referential Integrity



The following orphan records must be rejected or quarantined:



```text

Claim → nonexistent Policy

Claim → nonexistent Customer

Coverage → nonexistent Policy

ClaimEvent → nonexistent Claim

RiskScore → nonexistent Claim

