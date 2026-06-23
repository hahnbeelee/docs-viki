# Source: https://docs.developer.yelp.com/reference/v3_autocomplete

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of Yelp Places API, visit [Yelp Places API](https://docs.developer.yelp.com/docs/fusion-intro) to learn more.

text

string

required

length ≥ 1

Search text

locale

string

Locale code in the format of {language code}\_{country code}. See the [list of supported locales](https://docs.developer.yelp.com/docs/resources-supported-locales).

latitude

number

\-90 to 90

Required, if _location_ is not provided. Latitude of the location to search from. If latitude is provided, longitude is required too.

longitude

number

\-180 to 180

Required if _location_ is not provided. Longitude of the location to search from. If longitude is provided, latitude is required too.

# 

200

Autocomplete data returned.

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