\# API Contract



\## Purpose



This document defines the initial REST API contract for the Insurance

Claims Intelligence \& Automation Platform.



The backend implementation must follow these contracts.



Any breaking API change must be discussed before implementation and

documented here.



\---



\# API Version



Initial API version:



/api/v1



\---



\# Authentication



\## POST /api/v1/auth/login



Authenticates an application user.



\### Request



```json

{

&#x20; "username": "claims.analyst",

&#x20; "password": "example-password"

}

