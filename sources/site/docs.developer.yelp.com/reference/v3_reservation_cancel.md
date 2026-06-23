# Source: https://docs.developer.yelp.com/reference/v3_reservation_cancel

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

reservation\_id

string

required

# 

200

Success

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

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 404 | INVALID\_RESERVATION\_ID | The Reservation ID you provided is not valid. |

# 

409

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 409 | RESERVATION\_ALREADY\_CANCELED | This reservation has already been canceled. |
| 409 | RESERVATION\_CANCEL\_CONFLICT | The reservation could not be canceled due to a conflict. |

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

# 

503

Service Unavailable

Updated 10 months ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200400 - Invalid Request401 - Unauthorized401 - Invalid Token404409429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated 10 months ago

---