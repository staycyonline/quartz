See Also: https://portswigger.net/web-security/all-labs#os-command-injection and other injection attacks

FInd best requests to attack
 - FUzz and see responses
- Verbose reponse , errors, 
- find right payload to send for fuzz based on recon
- 
 Fuzzing is all about requesting the unexpected. When reviewing API documentation, if the API is expecting a certain type of input (number, string, boolean value) send:

- A very large number
- A very large string
- A negative number
- A string (instead of a number or boolean value)
- Random characters
- Boolean values
- Meta characters

---
## Metacharacters

Examples

`'`

`''`

`;%00`

`--`

`-- -`

`""`

`;`

`' OR '1`

`' OR 1 -- -`

`" OR "" = "`

`" OR 1 = 1 -- -`

`' OR '' = '`

`OR 1=1`

---
Collection runner can help running things over entire collection
while WFUZZ or fuff and burp can be good for individual requests

Candidate requests for attack include ones that take user input and probably interact with database

Make sure all endpoint run as expected - test for 200 ok and make sure all auth token is set
