# Source: https://docs.developer.yelp.com/reference/v3_business_match

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

> ## 📘
> 
> This endpoint is part of Yelp Places API, visit [Yelp Places API](https://docs.developer.yelp.com/docs/fusion-intro) to learn more.

name

string

required

length ≤ 64

The name of the business. Only digits, letters, spaces, and !#$%&+,./:?@'are allowed.

address1

string

required

length ≤ 64

The first line of the business's address. Only digits, letters, spaces, and '/#&,.: are allowed. An empty string is allowed; this will specifically match certain service businesses that have no street address.

address2

string

length ≤ 64

The second line of the business's address. Only digits, letters, spaces, and '/#&,.: are allowed.

address3

string

length ≤ 64

The third line of the business's address. Only digits, letters, spaces, and '/#&,.: are allowed.

city

string

required

length between 1 and 64

The city of the business. Only digits, letters, spaces, and '.() are allowed.

state

string

required

length between 1 and 3

The [ISO 3166-2](https://en.wikipedia.org/wiki/ISO_3166-2) (with a few [exceptions](https://docs.developer.yelp.com/docs/resources-state-codes)) state code of this business.

country

string

required

length between 2 and 2

The [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) country code of this business.

postal\_code

string

length ≤ 12

The [Zip code](https://en.wikipedia.org/wiki/Postal_code) of this business.

latitude

number

\-90 to 90

Required, if _location_ is not provided. Latitude of the location to search from. If latitude is provided, longitude is required too.

longitude

number

\-180 to 180

Required if _location_ is not provided. Longitude of the location to search from. If longitude is provided, latitude is required too.

phone

string

length between 1 and 32

The phone number of the business which can be submitted as 
(a) locally formatted with digits only (e.g., 016703080) or 
(b) internationally formatted with a leading + sign and digits only after (+35316703080).

yelp\_business\_id

string

length between 22 and 22

Unique Yelp identifier of the business if available. Used as a hint when finding a matching business.

limit

integer

1 to 10

Defaults to 3

Number of results to return.

match\_threshold

string

enum

Defaults to default

Specifies whether a match quality threshold should be applied to the matched businesses. Must be one of the following. 
**none:** Do not apply any match quality threshold; all potential business matches will be returned. 
**default:** Apply a match quality threshold such that only very closely matching businesses will be returned. 
**strict:** Apply a very strict match quality threshold.

nonedefaultstrict

Allowed:

`none``default``strict`

# 

200

One more more businesses were found.

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

413

The length of the request exceeded the maximum allowed

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

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

xxxxxxxxxx

1

curl \--request GET \\

2

 \--url 'https://api.yelp.com/v3/businesses/matches?limit=3&match\_threshold=default' \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found413 - Payload Too Large429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated 10 months ago

---

Did this page help you?

Yes

No