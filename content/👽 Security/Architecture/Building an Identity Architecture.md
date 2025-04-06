https://www.udemy.com/course/building-an-identity-architecture/
# Neo Security Architecture
---
Security components are broken into pieces which can do their things well and integrate well with one another using open standards

Open standards
- oauth
- openapi
- openid connect
- scim

Using open standards is best as it comes with less issues and confirm to standards, also prevents vendor locking - stays compliant to regulations like PSD2 or GDPR or CCPA

> [! info] The Architecture follows the core principle of separation of concerns

### Three pillars
---

![[Pasted image 20250406132434.png]]
#### Identity management
---
- **Identity store**
	- Securely store user data - data needed for authz and authn - data like roles,status - eg DB or AD
		
- **Profile services**
	- Frontend to identity store - enables to manage and update identity
	- SCIM standard is popular (https://scim.cloud/)
	- Exposes an API for others to consume without the need to know what the Identity store is
		
-  **Authentication service**
	- Authenticate the user - performs actions to enable to connect an entry from identity store to the request - the auth services will issue claims about users that others can trust
	- Popular standards - U2F, TOTP, WebAuthn
	- Auth is not standardized as a whole
	- Modern auth is complex
		- multi Factor Auth
		- time based filtering
		- Geolocation filtering
- **Token service**
	- Issue secure token - should be kept separate from authn service
	- generates token to user
	- access token, id token, refresh token - takes care of how long can it be valid
	- issue an opaque token or JWT
	- Which assertions / claims can mapped to the token 
	- Popular Standards: Auth2.0, OpenID Connect, JWT
	- Tokens can be issued by a [[Federation]] service using SAML or WS-Federation


![[Pasted image 20250406132310.png]]

#### API Management
---

![[Pasted image 20250406132518.png]]

- **API Gateway**
	- reverse proxy on steroids
	- Validates - path, method, access token and scopes of the request

	![[Pasted image 20250406132817.png]]
	- Can also have features like
		-  rate-limiting
		- centralized traffic metrics
		- phantom token flow or split token flow

	- Avoid adding too much project-specific code in gateway to prevent to being stuck with the product

- **API Management Platform** 
	- Define APIs and configs
	- Feeds gateway with config needed validation of requests
	- Some provide a portal for management
	
#### Entitlement management

Three levels of Authorization Applied in the below Architecture
 ![[Pasted image 20250406134324.png]]


![[Pasted image 20250406134421.png]]

![[Pasted image 20250406134432.png]]


![[Pasted image 20250406134512.png]]


When a system grows it becomes cumbersome to keep track of all the authorization policies and will require a system for book keeping to keep track and management - this is why an entitlement management system comes into play

![[Pasted image 20250406134850.png]]

- It Abstracts all policies to a centralized system - it can be managed using a policy administration point
- The points where the checks take place will become the enforcement point
- The enforcement point will query the policy decision point when a decision is to be made regarding a policy.
- The decision point uses the definitions stored in policy information point to make the decision
- This is useful in large systems - but complex for small systems
- Popular policy: Open Policy Agent


Next : [[API Integration Patterns]]
