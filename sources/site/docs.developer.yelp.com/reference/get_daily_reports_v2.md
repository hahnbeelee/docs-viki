# Source: https://docs.developer.yelp.com/reference/get_daily_reports_v2

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

> ## 🚧
> 
> Reporting API V2 is deprecated
> 
> Please migrate to [Reporting API V3](https://docs.developer.yelp.com/docs/reporting-v2-to-v3-migration-guide).

report\_id

string

required

The Report ID from [create\_daily\_reports\_v2](https://docs.developer.yelp.com/reference/create_daily_reports_v2).

# 

200

200

# 

202

Job Not Complete

# 

400

Bad Request. Message varies depending on failure scenario

# 

401

Authentication Error

# 

403

Authorization Error

# 

404

Resource Not Found

# 

413

The number of businesses in the request exceeded the maximum {max\_allowed\_businesses}

# 

429

Too Many Requests

# 

500

Internal Server Error

# 

503

Service Unavailable

Updated over 2 years ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

:

xxxxxxxxxx

1

curl \--request GET \\

2

 \--url https://partner-api.yelp.com/analytics/v2/businesses/daily\_reports/report\_id \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result202 - Job Not Complete400 - Invalid Request401403404413429500 - Internal Server Error503

Updated over 2 years ago

---

Did this page help you?

Yes

No