# Guidewire / Insurance Domain Mapping



**Owner:** Koundinya  

**Status:** Conceptual Domain Mapping  

**Version:** 1.0



\---



## 1. Purpose



This document describes how the platform's synthetic insurance-domain

model conceptually relates to common Guidewire InsuranceSuite domain

areas.



This project does not currently have access to a licensed Guidewire

environment or production Guidewire APIs.



Therefore, this document must not be interpreted as evidence of direct

Guidewire integration.



The mapping is intended to demonstrate insurance-domain understanding

and provide an integration boundary for possible future authorized

integration.



\---



# 2. Guidewire Product Context



Guidewire InsuranceSuite includes solutions addressing major insurance

business functions.



For this project, the most relevant conceptual areas are:



\- Policy administration

\- Claims management

\- Billing/payment-related information



The project primarily focuses on policy and claims intelligence.



\---



# 3. Conceptual Domain Mapping



| Platform Domain | Insurance Concept | Guidewire Conceptual Area |

|---|---|---|

| Customer | Insurance customer | Customer/account-related concept |

| Policy | Insurance policy | Policy administration |

| PolicyType | Product/policy type | Policy product concept |

| PolicyCoverage | Coverage | Policy coverage concept |

| Claim | Insurance claim | Claims management |

| ClaimEvent | Claim lifecycle event | Claims workflow/event concept |

| RiskScore | Analytical risk assessment | External analytics/decision-support concept |

| Premium | Policy premium | Policy/billing-related concept |

| Settlement | Claim settlement | Claims management |



These are conceptual mappings rather than direct API/entity mappings.



\---



# 4. Policy Domain



The platform represents a policy using:



\- policy\_id

\- policy\_number

\- customer\_id

\- policy\_type\_id

\- status

\- start\_date

\- end\_date

\- premium\_amount



A policy may contain multiple coverage records.



Conceptually:



```text

Customer

&#x20;  |

&#x20;  +---- Policy

&#x20;           |

&#x20;           +---- Policy Type

&#x20;           |

&#x20;           +---- Coverage

&#x20;           |

&#x20;           +---- Premium

