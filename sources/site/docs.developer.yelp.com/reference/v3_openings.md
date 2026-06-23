# Source: https://docs.developer.yelp.com/reference/v3_openings

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

business\_id\_or\_alias

string

required

A unique identifier for a Yelp Business. Can be either a 22-character Yelp Business ID, or a Yelp Business Alias.

covers

integer

required

1 to 10

How many people are attending the reservation (min. value is 1; max value is 10).

date

string

required

The date for the reservation, format is YYYY-mm-dd

time

string

required

The time of the requested reservation, format is HH:MM

get\_covers\_range

boolean

If true, include the covers\_range dict in the response.

truefalse

# 

200

Success

# 

400

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 400 | DATE\_TIME\_VALIDATION\_ERROR | Invalid format, expected format is %H:%M |
| 400 | DATE\_TIME\_VALIDATION\_ERROR | Invalid format, expected format is %Y-%m-%d |
| 400 | TOO\_SMALL\_VALIDATION\_ERROR | Number too small: {value} |
| 400 | TOO\_LARGE\_VALIDATION\_ERROR | Number too big: {value} |

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

Updated over 1 year ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - BookingsOpeningsResponseExample400401 - Unauthorized401 - Invalid Token404 - Resource Not Found429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated over 1 year ago

---