# Source: https://docs.developer.yelp.com/reference/remove-phone-numbers

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

Request body for removing outbound phone numbers.

phone\_numbers

object

required

phone\_numbers object

# 

200

The phone numbers were successfully removed

# 

400

This error is returned when one of the provided phone numbers is invalid.

| code | description |
| --- | --- |
| INVALID\_FORMAT | One or more phone numbers provided are in an invalid format. |

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

200 - PhoneNumbers400 - Invalid Format401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found429 - Rate limited500 - Internal Server Error

Updated 2 months ago

---