# Source: https://docs.developer.yelp.com/reference/v3_business_waitlist_on-my-way-1

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

business\_id

string

required

Encrypted Yelp business identifer

The request body for creating an on-my-way visit

phone

string

required

Patron's phone number in E.164 format

party\_size

integer

required

Number of guests in the party

name

string

required

Patron's name

arrival\_range\_max

integer

required

Patron's expected maximum arrival time (in minutes). Must be 30 minutes from now or earlier. Should be the upper bound of the arrival estimate selected.

arrival\_range\_min

integer

required

Patron's expected minimum arrival time (in minutes). Must be 30 minutes from now or earlier.

party\_notes

string

Notes from the patron. Will be visible to the host in the host app.

# 

201

An object contains information about the created on-my-way visit

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
| 409 | CONFLICT | On My Way active visit limit reached (max is currently 9 active on-my-way visits per restaurant) |

# 

422

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 422 | ALREADY\_IN\_LINE | Invalid state. For example, the phone number is already in line |
| 422 | INVALID\_ETA | Expected arrival time too far in the past or future. Must be 30 minutes from now or earlier. |
| 422 | CURRENTLY\_HAS\_WAIT | On My Way visit creation is ineligible, there is currently a wait for the restaurant. |
| 422 | PARTY\_SIZE\_TOO\_LARGE | Party size too large. |
| 422 | RESTAURANT\_NOT\_OPEN | Restaurant is not open. |
| 422 | REMOTE\_ENTRY\_DENIED | Restaurant does not allow remote entry. |
| 422 | SCHEDULE\_CONFLICT | Special event at restaurant. |

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

201 - Result400 - Invalid Request401 - Unauthorized401 - Invalid Token404 - Resource Not Found409422429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated about 2 years ago

---