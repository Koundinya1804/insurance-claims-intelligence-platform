\# Data Contract



\## Purpose



Defines the minimum expectations for data entering the platform.



\---



\## Supported Initial Sources



\- CSV

\- JSON



The initial datasets are synthetic.



No real customer or insurance data will be used.



\---



\## Required Dataset Categories



\### Customers



Required fields:



\- customer\_id

\- first\_name

\- last\_name

\- date\_of\_birth

\- customer\_type

\- region



\### Policies



Required fields:



\- policy\_id

\- policy\_number

\- customer\_id

\- policy\_type\_id

\- status

\- start\_date

\- end\_date

\- premium\_amount



\### Claims



Required fields:



\- claim\_id

\- policy\_id

\- customer\_id

\- claim\_type

\- status

\- claim\_amount

\- claim\_date

\- location



\---



\## Data Quality Rules



The pipeline must validate:



\- required fields

\- data types

\- duplicate records

\- duplicate identifiers

\- valid customer references

\- valid policy references

\- valid claim statuses

\- valid policy statuses

\- valid dates

\- non-negative monetary amounts

\- orphan records



\---



\## Data Processing Zones



Raw

↓

Validated

↓

Curated

↓

Database / Analytics



\---



\## Data Quality Metrics



The pipeline should report actual measured values for:



\- records received

\- records accepted

\- records rejected

\- duplicates

\- missing required fields

\- invalid references

\- invalid values



No example metric may be presented as an actual project metric.

