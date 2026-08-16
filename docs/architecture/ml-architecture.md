# Insurance Claims Intelligence & Automation Platform



## ML Architecture



\*\*Owner:\*\* Saad Ahmed



\*\*Technical/Domain Contributor:\*\* Koundinya



\*\*Status:\*\* ML Architecture Baseline



\*\*Version:\*\* 1.0



\---



# 1. Purpose



This document defines the Machine Learning architecture for the Insurance Claims Intelligence & Automation Platform.



The ML component provides claim risk scoring and analytical decision support.



The architecture covers:



\- Data preparation

\- Feature engineering

\- Model training

\- Model evaluation

\- Model versioning

\- Model inference

\- Risk-score persistence

\- API integration

\- Analytics integration

\- Explainability

\- Monitoring

\- Retraining



The architecture does not claim that a production ML model has already been trained or deployed.



\---



# 2. ML Objective



The initial ML objective is to estimate the relative risk associated with an insurance claim.



The model may use features such as:



\- Claim amount

\- Claim type

\- Previous claim count

\- Claim frequency

\- Policy age

\- Customer claim history

\- Time between claims



The model output is intended to support human decision-making.



The model must not independently:



\- Approve a claim

\- Reject a claim

\- Settle a claim

\- Determine fraud conclusively



\---



# 3. ML Contract



The ML implementation shall follow:



`docs/contracts/ml-contract.md`



The contract defines the expected interface between the ML component and the rest of the platform.



The ML architecture must not introduce a conflicting risk-score format or lifecycle.



\---



# 4. High-Level Architecture



```text

              Curated Claims Data

                       |

                       v

                Feature Pipeline

                       |

                       v

                  Feature Set

                       |

             +---------+---------+

             |                   |

             v                   v

        Model Training      Data Validation

             |

             v

        Model Evaluation

             |

       +-----+-----+

       |           |

       v           v

   Model Pass   Model Fail

       |

       v

 Model Artifact

       |

       v

 Model Version

       |

       v

 ML Inference

       |

       v

 Risk Score

       |

   +---+---+

   |       |

   v       v

FastAPI  PostgreSQL

   |       |

   +---+---+

       |

       v

   Analytics

       |

       v

    Power BI


