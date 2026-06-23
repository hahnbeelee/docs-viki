# Source: https://docs.developer.yelp.com/reference/get_monthly_reports_v3

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the Reporting API, visit [Reporting API](https://docs.developer.yelp.com/docs/reporting-api) to learn more.

report\_id

string

required

The Report ID from [create\_monthly\_reports\_v3](https://docs.developer.yelp.com/reference/create_monthly_reports_v3).

# 

200

Report generated successfully.

# 

202

The requested report job is not complete yet or the report failed.

| code | description |
| --- | --- |
| JOB\_NOT\_COMPLETE | Job Not Complete. |
| JOB\_FAILED | Job Failed. Please note that if a job failed because of authorization issues, the endpoint will raise a 403 - Forbidden with the code AUTHORIZATION\_ERROR |

# 

400

Bad Request. Message varies depending on failure scenario

| code | description |
| --- | --- |
| VALIDATION\_ERROR | Validation Error. |
| INVALID\_REPORT\_ID | Invalid Request |
| REPORT\_GRANULARITY\_ERROR | Invalid report granularity requested. Attempted to retrieve a monthly report, on a daily endpoint. Please request the report on a monthly endpoint. |

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

403

Authorization Error or Partner API endpoint disabled.

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated over 2 years ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result202 - JOB NOT COMPLETE202 - JOB FAILED400 - INVALID REPORT ID400 - REPORT GRANULARITY ERROR401 - Unauthorized401 - Invalid Token403 - Authorization Error403 - Endpoint Disabled429 - Rate limited500 - Internal Server Error

Updated over 2 years ago

---