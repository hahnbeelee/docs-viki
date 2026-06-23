# Source: https://docs.developer.yelp.com/reference/v3_get_jobs

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

Request object for getting jobs based on natural language query.

query

string

required

length ≤ 1000

Natural language text describing the needs.

locale

string

Defaults to en\_US

Locale code in the format of {language code}\_{country code}. See the [list of supported locales](https://docs.developer.yelp.com/docs/resources-supported-locales).

# 

200

Successfully retrieved jobs

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

Updated 4 months ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found429 - Rate limited500 - Internal Server Error

Updated 4 months ago

---