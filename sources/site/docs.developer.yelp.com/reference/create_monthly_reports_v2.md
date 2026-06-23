# Source: https://docs.developer.yelp.com/reference/create_monthly_reports_v2

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 🚧
> 
> Reporting API V2 is deprecated
> 
> Please migrate to [Reporting API V3](https://docs.developer.yelp.com/docs/reporting-v2-to-v3-migration-guide).

start

string

required

Start month. (Format `YYYY-MM`)

end

string

required

End month. (Format `YYYY-MM`)

ids

array of strings

required

A list of Yelp Business IDs

ids\*

ADD string

metrics

array of strings

required

Business and Advertising Metrics to be included in report. 
See [Business Metrics](https://docs.developer.yelp.com/docs/reporting-api#business-metrics) and [Advertiser Metrics](https://docs.developer.yelp.com/docs/reporting-api#advertiser-metrics) for a detailed description of all available metrics.

metrics\*

Show 53 enum values

ADD string

# 

200

200

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

ShellNodeRubyPHPPython

:

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Report created successfully400 - Invalid Request401403404413429500 - Internal Server Error503

Updated over 2 years ago

---