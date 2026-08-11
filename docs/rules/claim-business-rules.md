\# Claim Business Rules



\*\*Owner:\*\* Koundinya



\---



\# 1. Purpose



Defines insurance-specific business rules for claims processing.



These rules represent the synthetic insurance domain implemented by the

platform.



They are independent of any specific programming language or database

implementation.



\---



\# 2. Claim Identity



\### BR-CLM-001



Every claim must have a unique claim\_id.



\### BR-CLM-002



Every claim must have a unique claim number where claim numbers are

used as business identifiers.



\---



\# 3. Policy Relationship



\### BR-CLM-003



Every claim must reference an existing policy.



\### BR-CLM-004



The customer associated with a claim must match the customer associated

with the referenced policy.



\### BR-CLM-005



A claim cannot be created against a nonexistent policy.



\---



\# 4. Claim Amount



\### BR-CLM-006



Claim amount must be greater than or equal to zero.



\### BR-CLM-007



Currency values must use a consistent currency representation.



\---



\# 5. Claim Date



\### BR-CLM-008



Claim date must be a valid date.



\### BR-CLM-009



The claim date must satisfy the applicable policy validity rules.



The exact implementation should define how claims outside the policy

period are handled.



\---



\# 6. Claim Status



\### BR-CLM-010



A claim must always have one valid canonical status.



Allowed statuses:



\- FILED

\- UNDER\_REVIEW

\- INVESTIGATION

\- APPROVED

\- REJECTED

\- SETTLED



\---



\# 7. State Transitions



\### BR-CLM-011



Only valid claim state transitions are allowed.



\### BR-CLM-012



FILED may transition to UNDER\_REVIEW.



\### BR-CLM-013



UNDER\_REVIEW may transition to INVESTIGATION.



\### BR-CLM-014



INVESTIGATION may transition to APPROVED or REJECTED.



\### BR-CLM-015



APPROVED may transition to SETTLED.



\### BR-CLM-016



Rejected claims cannot transition directly to SETTLED.



\### BR-CLM-017



Settled claims cannot transition back into investigation.



\---



\# 8. Settlement



\### BR-CLM-018



Settlement date must only be recorded when a claim reaches settlement.



\### BR-CLM-019



Settlement date must not precede claim date.



\### BR-CLM-020



A rejected claim cannot have a successful settlement state.



\---



\# 9. Claim Events



\### BR-CLM-021



A valid claim status transition should generate a ClaimEvent.



\### BR-CLM-022



Claim events should preserve:



\- previous status

\- new status

\- timestamp

\- actor

\- notes where applicable



\---



\# 10. Risk Assessment



\### BR-CLM-023



Risk scoring is decision support.



\### BR-CLM-024



Risk scoring must not automatically approve or reject a claim.



\### BR-CLM-025



Risk score must be represented between 0 and 100.



\### BR-CLM-026



Risk levels are:



\- LOW

\- MEDIUM

\- HIGH



\### BR-CLM-027



Risk explanations must be based on actual model inputs or a valid

explainability mechanism.



\---



\# 11. Data Quality



\### BR-CLM-028



Duplicate claim identifiers must be rejected or quarantined by the data

pipeline.



\### BR-CLM-029



Claims with invalid customer references must not enter the curated

dataset.



\### BR-CLM-030



Claims with invalid policy references must not enter the curated

dataset.



\---



\# 12. Synthetic Data



\### BR-CLM-031



Only synthetic insurance data may be used in this project.



\---



\# 13. Business Rule vs Technical Implementation



These rules define business meaning.



Implementation may occur through:



\- database constraints

\- Pydantic validation

\- service-layer rules

\- ETL validation

\- API validation

\- automated tests



The technical implementation must not silently change the business

meaning of these rules.

