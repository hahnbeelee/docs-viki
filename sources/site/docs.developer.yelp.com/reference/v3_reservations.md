# Source: https://docs.developer.yelp.com/reference/v3_reservations

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

The request object for placing a reservation on a requested time slot.

covers

integer

1 to 10

How many people are attending the reservation (min. value is 1; max value is 10).

date

string

required

The date for the reservation, format is YYYY-mm-dd

time

string

required

The time of the requested reservation, format is HH:MM.

first\_name

string

required

The first name of the person making the reservation.

last\_name

string

required

The last name of the person making the reservation.

phone

string

required

length between 1 and 32

The phone number to attach to the reservation.

email

string

required

The email to attach to the reservation.

hold\_id

string

required

The Hold ID returned from the Holds endpoint.

unique\_id

string

required

length ≤ 300

This should be the user's device id or a unique user id to help tie together actions of the user on the API. Multiple requests to the Holds endpoint by the same user should use the same unique\_id.

notes

string

The additional party notes for the reservation.

# 

200

Success

# 

400

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 400 | INVALID\_RESERVATION\_PARAMETER | One of the following: 
\- Time must be 0, 15, 30 or 45 
\- date too far out in the future 
\- date is in the past 
\- This restaurant accepts reservations {max\_future\_days} days in the future (NOTE: The {max\_future\_days} will be dependent on the restaurant's setting) 
\- This restaurant only accepts online reservations between {minvalue} and {max\_value} people (NOTE: The {min\_value} and {max\_value} will be dependent on the restaurant's accepted minimum and maximum values for their online reservations) 
\- Bad request |
| 400 | DATE\_TIME\_VALIDATION\_ERROR | Invalid format, expected format is %H:%M |
| 400 | DATE\_TIME\_VALIDATION\_ERROR | Invalid format, expected format is %Y-%m-%d |
| 400 | TOO\_SMALL\_VALIDATION\_ERROR | Number too small: {value} |
| 400 | TOO\_LARGE\_VALIDATION\_ERROR | Number too big: {value} |
| 400 | INVALID\_HOLD\_ID | The Hold ID you provided is not valid. |
| 400 | RESERVATIONS\_PARAMS\_DONT\_MATCH\_HOLDS\_PARAMS | Input parameters must match the values provided to the Holds endpoint. |

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

402

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 402 | CREDIT\_CARD\_REQUIRED | This reservation requires a credit card hold. Please contact the restaurant or use the reservation URL provided |

# 

404

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 404 | BUSINESS\_NOT\_FOUND | The requested business could not be found. |
| 404 | DOES\_NOT\_TAKE\_RESERVATIONS | The given business does not take reservations. |
| 404 | HOLD\_NOT\_FOUND | No valid hold found corresponding to the hold ID you provided. A hold with this ID may have never existed, or it may have expired. |

# 

409

This error is returned in any of the following scenarios:

| Status | error\_code | Reason |
| --- | --- | --- |
| 409 | RESERVATION\_SLOT\_NO\_LONGER\_AVAILABLE | The time you requested to book a reservation for is no longer available. Please try to reserve a different time. |
| 409 | DUPLICATE\_RESERVATION | You already have a reservation for that day. |

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

200400401 - Unauthorized401 - Invalid Token402404409429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated over 1 year ago

---