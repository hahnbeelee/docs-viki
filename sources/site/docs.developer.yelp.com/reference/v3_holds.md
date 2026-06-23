# Source: https://docs.developer.yelp.com/reference/v3_holds

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

The request object for placing a temporary hold on a requested time slot.

covers

integer

required

1 to 10

How many people are attending the reservation.

date

string

required

The date for the reservation, format is YYYY-mm-dd

time

string

required

The time of the requested reservation, format is HH:MM.

unique\_id

string

required

length ≤ 300

This should be the user's device id or a unique user id to help tie together actions of the user on the API. Multiple requests to the Holds endpoint by the same user should use the same unique\_id.

# 

200

Success

# 

400

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 400 | COVERS\_VALUE\_OUT\_OF\_RANGE | This restaurant only accepts online reservations between {minvalue} and {max\_value} people. NOTE: The {min\_value} and {max\_value} will be dependent on the restaurant's accepted minimum and maximum values for their online reservations. |
| 400 | INVALID\_DATE\_TIME\_RANGE | The date time range is invalid |
| 400 | INVALID\_RESERVATION\_PARAMETER | Bad request |
| 400 | TOO\_LARGE\_VALIDATION\_ERROR | Number too big: {value} |
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

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 404 | BUSINESS\_NOT\_FOUND | The requested business could not be found. |
| 404 | DOES\_NOT\_TAKE\_RESERVATIONS | The given business does not take reservations. |

# 

409

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 409 | HOLD\_SLOT\_NOT\_AVAILABLE | The requested hold time is not available. Please select a different time. |

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

200400401 - Unauthorized401 - Invalid Token404409429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated over 1 year ago

---