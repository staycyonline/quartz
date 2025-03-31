Unsupported versions must not be available for consumption

Often times an API provider will update services and the newer version of the API will be available over a new path like the following:

- api.target.com/v3
- /api/v2/accounts
- /api/v3/accounts
- /v2/accounts

API versioning could also be maintained as a header:

- _Accept: version=2.0_
- _Accept api-version=3_

In addition versioning could also be set within a query parameter or request body.

- /api/accounts?ver=2
- POST /api/accounts  
      
    {  
    "ver":1.0,  
    "user":"hapihacker"  
    }

---
Postman Collection Runner
 - tests in collections settings
 - test as both authorized and non auth
 - replace version with different version nos
 - watch for different behavior between versions