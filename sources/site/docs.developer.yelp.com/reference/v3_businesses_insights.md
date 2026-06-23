# Source: https://docs.developer.yelp.com/reference/v3_businesses_insights

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

business\_ids

array of strings

required

length ≤ 20

Business Id or alias of the businesses for which to get data

business\_ids\*

ADD string

date\_range\_start

string

required

Start of the date range during which to get data. Accepted format is "YYYYMM".

date\_range\_end

string

required

End of the date range during which to get data. Accepted format is "YYYYMM".

# 

200

Business Insights for one or more businesses were returned.

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

 \--url https://api.yelp.com/v3/businesses/insights \\

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