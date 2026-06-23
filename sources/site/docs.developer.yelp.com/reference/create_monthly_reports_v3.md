# Source: https://docs.developer.yelp.com/reference/create_monthly_reports_v3

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the Reporting API, visit [Reporting API](https://docs.developer.yelp.com/docs/reporting-api) to learn more.

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

202

202 - Accepted

# 

400

Bad Request. Message varies depending on failure scenario

| code | description |
| --- | --- |
| VALIDATION\_ERROR | Validation Error. |
| INVALID\_REQUEST | Invalid Request. |
| MAX\_NUM\_OF\_DAILY\_LOOKBACK\_ERROR | The number of days to look up monthly business metrics exceeded the maximum (730). Please use a start date less than 730 days from now |
| MAX\_NUM\_OF\_MONTHS\_RANGE\_ERROR | The date range for monthly business metrics exceeded the maximum (3 months). Please use a date range of less than 3 months |
| END\_DATE\_EARLIER\_THAN\_START\_DATE | The start date has to be earlier or equal to the end date. |

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

403

Partner API endpoints require set up by Yelp before they can be used. You are trying to access a Partner API endpoint for which your API Client has not been enabled. Please reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) for more information.

# 

413

The number of businesses in the request exceeded the maximum (500)

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated 2 months ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

202 - Report created successfully400 - INVALID REQUEST400 - MAX NUM OF DAILY LOOKBACK ERROR400 - MAX NUM OF MONTHS RANGE ERROR400 - END DATE EARLIER THAN START DATE401 - Unauthorized401 - Invalid Token403 - Endpoint Disabled413 - NUMBER OF BUSINESS LIMIT ERROR429 - Rate limited500 - Internal Server Error

Updated 2 months ago

---