Authorization vulns are very common

try removing cookie and see if we can access unauthenticated

Broken Object Level Authorization (BOLA) and Broken Function Level Authorization (BFLA) are in OWASP API top ten

BOLA - no restriction to other user resources (eg: seeing other users account details without authz)
BFLA -  no restriction in action that can manipulate other users resources (eg:being able to send money from ohter users account without authz)


## BOLA
---
Able to interact with resources of other users without authz

Recipie for BOLA
 - resource id
 - Requests that access resources
 - Missing access control

FIrst two can be discovered in documentation while third must be tested

A B testing - fetch resources with user A and see if we can get restricted resources of A using account B

use [[Excessive Data Exposure]] vuln to get more object IDs for testing


## BFLA
---
Unauth actions
 - lateral actions
 - escalated actions

Users should be able to delete their profile pic but not others

- resource id
- requests with flawed access controls
- endpoints that person authorized actions

Create, update and delete actions are of focus here. Also admin actions as well

A-B-A testing