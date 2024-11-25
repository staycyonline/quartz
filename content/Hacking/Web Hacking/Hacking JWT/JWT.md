JWT consists of header payload and signature

Header and Payload are base 64 encoded objects.

Header contains metadata about the token

Payload contains the claims about the user (data)

The server that issues the token typically generates the signature by hashing the header and payload. In some cases, they also encrypt the resulting hash. Either way, this process involves a secret signing key. This mechanism provides a way for servers to verify that none of the data within the token has been tampered with since it was issued