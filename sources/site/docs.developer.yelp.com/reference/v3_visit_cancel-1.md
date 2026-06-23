# Source: https://docs.developer.yelp.com/reference/v3_visit_cancel-1

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

visit\_id

string

required

Encrypted Yelp visit identifer

# 

204

The visit is canceled successfully

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

409

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 409 | VISIT\_ALREADY\_IN\_TERMINAL\_STATE | This visit was already in a terminal state or the customer is not in queue |

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

204400 - Invalid Request401 - Unauthorized401 - Invalid Token404 - Resource Not Found409429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated about 2 years ago

---