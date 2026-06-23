# Source: https://docs.developer.yelp.com/reference/v3_business_reviews

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of Yelp Fusion, visit [Yelp Places API](https://docs.developer.yelp.com/docs/fusion-intro) to learn more. To access this endpoint, you require either the [Enhanced Plan or Premium Plan](https://docs.developer.yelp.com/business.yelp.com/data/products/places-api/) permission.

business\_id\_or\_alias

string

required

A unique identifier for a Yelp Business. Can be either a 22-character Yelp Business ID, or a Yelp Business Alias.

locale

string

Locale code in the format of {language code}\_{country code}. See the [list of supported locales](https://docs.developer.yelp.com/docs/resources-supported-locales).

offset

integer

0 to 1000

Offset the list of returned results by this amount.

limit

integer

0 to 50

Defaults to 20

Number of reviews to return.

sort\_by

string

enum

Defaults to yelp\_sort

Sort reviews by.

yelp\_sort

Allowed:

`yelp_sort`

# 

200

Returns up to three review excerpts for the given business.

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

The API key provided is not currently able to query this endpoint.

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