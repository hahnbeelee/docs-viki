# Source: https://docs.developer.yelp.com/reference/v3_get_businesses_engagement

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of Yelp Insights, visit [Yelp Insights API](https://docs.developer.yelp.com/business.yelp.com/data/products/insights-api/) to learn more.

business\_ids

array of strings

required

length ≤ 20

Business Id or alias of the businesses for which to get data.

business\_ids\*

ADD string

date\_range\_start

date

Start of the date range during which to get metrics. Defaults to the beginning of the most recently available week.

date\_range\_end

date

End of the date range during which to get metrics. Defaults to the end of the most recently available week.

# 

200

Engagement metrics for one or more businesses were returned.

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