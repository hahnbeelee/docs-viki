# Source: https://docs.developer.yelp.com/reference/v3_all_categories

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

locale

string

Specify the locale to filter the categories returned to only those available in that locale, and to translate the names of the categories appropriately. 
See the [list of supported locales](https://docs.developer.yelp.com/docs/resources-supported-locales). If not included, all categories across all locales will be returned and the category names will be in English.

# 

200

One or more categories were returned.

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

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

xxxxxxxxxx

1

curl \--request GET \\

2

 \--url https://api.yelp.com/v3/categories \\

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