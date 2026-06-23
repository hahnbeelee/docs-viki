# Source: https://docs.developer.yelp.com/reference/get-phone-numbers

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

limit

integer

1 to 500

Defaults to 100

Number of phone numbers to return. By default, it will return 100. Maximum is 500.

offset

integer

≥ 0

Defaults to 0

Offset the list of returned phone numbers by this amount.

# 

200

The phone numbers were returned successfully

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

403

Authorization Error

# 

404

Resource Not Found

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated 2 months ago

---

ShellNodeRubyPHPPython

Bearer

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Example response when the capability is enabled for the client200 - Example response when the capability is disabled for the client401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found429 - Rate limited500 - Internal Server Error

Updated 2 months ago

---