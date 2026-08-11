\# Insurance Claims Intelligence Platform



\# Entity Relationship Model



\*\*Owner:\*\* Koundinya  

\*\*Phase:\*\* 3  

\*\*Version:\*\* 1.0



\---



\# 1. Purpose



Defines the canonical logical relationships between the core insurance

entities.



\---



\# 2. Logical ER Model



```text

&#x20;                        ┌──────────────┐

&#x20;                        │   CUSTOMER   │

&#x20;                        │──────────────│

&#x20;                        │ customer\_id  │

&#x20;                        │ customer\_no  │

&#x20;                        └──────┬───────┘

&#x20;                               │

&#x20;                             1 │

&#x20;                               │ N

&#x20;                        ┌──────▼───────┐

&#x20;                        │    POLICY    │

&#x20;                        │──────────────│

&#x20;                        │ policy\_id    │

&#x20;                        │ customer\_id  │

&#x20;                        │ policy\_type  │

&#x20;                        │ status       │

&#x20;                        │ start\_date   │

&#x20;                        │ end\_date     │

&#x20;                        └───┬──────┬───┘

&#x20;                            │      │

&#x20;                          1 │      │ 1

&#x20;                            │      │

&#x20;                          N │      │ N

&#x20;                   ┌────────▼─┐  ┌─▼──────────────┐

&#x20;                   │ COVERAGE │  │     CLAIM      │

&#x20;                   │──────────│  │────────────────│

&#x20;                   │coverage\_id│ │ claim\_id       │

&#x20;                   │policy\_id │  │ policy\_id      │

&#x20;                   │limit     │  │ customer\_id    │

&#x20;                   │deductible│  │ status         │

&#x20;                   └──────────┘  │ claim\_amount   │

&#x20;                                 └───┬────────┬───┘

&#x20;                                     │        │

&#x20;                                   1 │        │ 1

&#x20;                                     │        │

&#x20;                                   N │        │ N

&#x20;                             ┌───────▼──┐  ┌──▼───────────┐

&#x20;                             │  CLAIM   │  │ RISK SCORE   │

&#x20;                             │  EVENT   │  │──────────────│

&#x20;                             │──────────│  │risk\_score\_id │

&#x20;                             │event\_id  │  │claim\_id      │

&#x20;                             │claim\_id  │  │risk\_score    │

&#x20;                             │old\_state │  │risk\_level    │

&#x20;                             │new\_state │  │model\_version │

&#x20;                             └──────────┘  └──────────────┘

