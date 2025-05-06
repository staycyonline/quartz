See Also : https://curity.io/resources/articles/

Introduction
Phantom Token Flow
Split Token Flow
Proof of Possession tokens

# Introduction
---

![[Pasted image 20250406144415.png]]

The token flow is implemented in the Token service and API gateway
Proof of possession can Implemented in the above but also in API services

# Phantom Token Flow
---

![[Pasted image 20250406145153.png]]

- Token services can use JWT or opaque token while issuing tokens
- Opaque token acts as an identifier in the token service to access the claims for the user
- JWT has the claims encoded into them and signed by a signature - so claims dont have to be persisted in the token service
- Use opaque tokens if they are available publicly - esp third-party clients 

### Why use opaque tokens? 

- Data in JWT is meant for API not client - if it is not meant for client then don't release it
- Data in JWT is public - signature is for integrity only
- Risk of damaging integrations with incompatible changes

The below flow demonstrates how Opaque token mitigates damage that can be caused by JWT

![[Pasted image 20250406150039.png]]

API services can use the opaque token to query the claims in the backend in json format

Disadvantage of this approach is that multiple API services might have to do multiple calls to the token service overloading the system

![[Pasted image 20250406150313.png]]

Phantom token flow mitigates that issue

![[Pasted image 20250406150439.png]]

Here the API gateway uses the opaque token to get a JWT with claims signed by the token service and this JWT is passed to all the services that are called. As it is signed the integrity can be assured and each service can access the claims in situ

![[Pasted image 20250406150832.png]]

This way we can use opaque tokens outside the infra and JWT inside  the infra

No of requests can be reduced by having a cache in the internal infra and can query the cache for the any request with the same opaque token

![[Pasted image 20250406151028.png]]

Caching can make it difficult to revoke the token - so the cache should have reasonably less expiration time or implement a mechanism for token service to invalidate a token in the cache

![[Pasted image 20250406151326.png]]

We can implement some validation in API gateway so that invalid requests can be rejected early without sending it inside the infra. Here , the gateway takes in both JWT and JSON with claims and can perform some validations from the gateway's end before forwarding the request.

Phantom token provides
- Better security and privacy
- Performance optimization
- Centralized validation or other features

# Split Token Flow
---
- Another variation of Phantom token flow
- Useful when caching is not an option due to security requirements - as cached tokens can be reused if the cache is compromised
- Gateway is spread across multiple data center and token service is centralized
- Reduces latency


![[Pasted image 20250406152013.png]]

- JWT is split into two
	 - signature 
	 - header + payload

- Signature is sent to client to use as an opaque token
- The header + body is stored in a cache with the hashed signature as the identifier
-  API gateway hashes the receives signature that comes with the request and looks up in the cache.
- API Gateway reconstructs the the JWT using the signature received from client and header and payload in the cache and shares it with the API
- This way neither the cache or the gateway has the whole JWT
- Mechanisms for token revocation should be implemented here as well

# Proof of Possession tokens
---
Two types
 - Bearer - bearer doesn't need to prove the ownership of the token
 - Proof of possession - can only be used by the client whom it was originally issued - hard to implemement

- PoP in JWT is defined  in RFC 7800 - cnf claim is added to JWT which can be used to verify the caller - this is usually a public key or identifier of the key

![[Pasted image 20250406155529.png]]

After verification the PoP token alone can be forwarded to the APIs

# Demonstration of Proof of Possession (DPOP) tokens ⚠️
---


![[Pasted image 20250406183834.png]]

![[Pasted image 20250406183937.png]]

# API Integration patterns
---
![[Pasted image 20250406184219.png]]

