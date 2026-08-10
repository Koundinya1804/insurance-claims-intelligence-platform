\# Machine Learning Contract



\## Purpose



This document defines the contract between the ML risk-scoring system

and the rest of the Insurance Claims Intelligence \& Automation Platform.



The initial ML capability is claim risk scoring.



The system must not claim to detect real insurance fraud unless the

training data and evaluation methodology genuinely support that claim.



\---



\# ML Objective



The model estimates the level of risk associated with an insurance

claim and helps prioritize claims for additional review.



The output is decision support.



It is not an autonomous claim approval, rejection, or fraud decision.



\---



\# Risk Score



The application exposes a normalized risk score:



0–100



Risk levels:



\- 0–30: LOW

\- 31–70: MEDIUM

\- 71–100: HIGH



The thresholds are application-level definitions and may be revisited

after model evaluation.



\---



\# Candidate Input Features



Potential features include:



\- claim\_amount

\- policy\_age\_days

\- previous\_claim\_count

\- claims\_last\_12\_months

\- days\_since\_previous\_claim

\- claim\_type

\- region

\- customer\_claim\_frequency



Features must only use information that would reasonably be available

at the time the risk assessment is performed.



\---



\# Data Leakage Prevention



The model must not use information that would only become available

after the prediction point.



Examples of potentially invalid prediction features include:



\- final settlement outcome

\- post-investigation findings

\- future claim events

\- information created after the risk assessment



The training pipeline must explicitly review features for potential

data leakage.



\---



\# Input Contract



A risk-scoring request should conceptually contain:



```json

{

&#x20; "claim\_id": "CL1001",

&#x20; "claim\_amount": 50000,

&#x20; "policy\_age\_days": 180,

&#x20; "previous\_claim\_count": 2,

&#x20; "claims\_last\_12\_months": 2,

&#x20; "days\_since\_previous\_claim": 120,

&#x20; "claim\_type": "AUTO\_ACCIDENT",

&#x20; "region": "HYDERABAD"

}

