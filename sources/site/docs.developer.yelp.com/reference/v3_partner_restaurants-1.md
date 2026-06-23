# Source: https://docs.developer.yelp.com/reference/v3_partner_restaurants-1

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

# 

200

An object contains a list of onboarded restaurants of the calling partner returned.

# 

400

Bad Request. Message varies depending on failure scenario

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

404

Resource Not Found

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

# 

503

Service Unavailable

Updated about 2 years ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Request401 - Unauthorized401 - Invalid Token404 - Resource Not Found429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated about 2 years ago

---