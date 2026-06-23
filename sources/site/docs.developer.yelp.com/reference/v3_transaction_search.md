# Source: https://docs.developer.yelp.com/reference/v3_transaction_search

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of Yelp Places API, visit [Yelp Places API](https://docs.developer.yelp.com/docs/fusion-intro) to learn more.

transaction\_type

string

enum

required

Defaults to delivery

Type of transaction supported by the business

delivery

Allowed:

`delivery`

latitude

number

\-90 to 90

Required, if _location_ is not provided. Latitude of the location to search from. If latitude is provided, longitude is required too.

longitude

number

\-180 to 180

Required if _location_ is not provided. Longitude of the location to search from. If longitude is provided, latitude is required too.

location

string

length between 1 and 250

Required if either _latitude_ or _longitude_ is not provided. 
This string indicates the geographic area to be used when searching for businesses. 
Examples: "New York City", "NYC", "350 5th Ave, New York, NY 10118". 
Businesses returned in the response may not be strictly within the specified location.

term

string

length ≤ 300

Search term, e.g. "food" or "restaurants". 
The term may also be the business's name, such as "Starbucks". If term is not included the endpoint will default to searching across businesses from a small number of popular categories.

categories

array of strings

Categories to filter the search results with. See the list of supported categories. The category filter can be a list of comma delimited categories. 
e.g., "bars,french" will filter by Bars OR French. 
The category alias should be used (e.g. "discgolf", not "Disc Golf").

categories

ADD string

price

array of integers

length ≤ 4

Pricing levels to filter the search result with: 1 = $, 2 = $$, 3 = $$$, 4 = $$$$. The price filter can be a list of comma delimited pricing levels. 
e.g., "1, 2, 3" will filter the results to show the ones that are $, $$, or $$$.

price

ADD integer

# 

200

Transaction data for one or more businesses was returned.

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

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Authorization Error404 - Resource Not Found413 - Payload Too Large429 - Rate limited500 - Internal Server Error503 - Service Unavailable

Updated 10 months ago

---