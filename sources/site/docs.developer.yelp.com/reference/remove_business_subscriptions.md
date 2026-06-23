# Source: https://docs.developer.yelp.com/reference/remove_business_subscriptions

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
> This endpoint is part of the Business Subscriptions API, visit [Business Subscriptions API](https://docs.developer.yelp.com/docs/business-subscriptions-api) to learn more.

# 

202

Request accepted. The business subscriptions will be removed asynchronously

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

This error is returned in any of the following scenarios:

- The API key provided is not currently able to query this endpoint or manage business subscriptions of a certain type
- Trying to access a Partner API endpoint for which the API Client has not been enabled
- The yearly remove quota for YELP\_KNOWLEDGE subscriptions would be exceeded with the incoming request.

| code | description |
| --- | --- |
| PARTNER\_ENDPOINT\_DISABLED | You are trying to access a Partner API endpoint for which your API Client has not been enabled. Please reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) for more information. |
| AUTHORIZATION\_ERROR | Authorization Error |
| QUOTA\_EXCEEDED | Exceeded the yearly remove quota. |

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated over 2 years ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

xxxxxxxxxx

1

curl \--request DELETE \\

2

 \--url https://api.yelp.com/v3/businesses/subscriptions \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

202400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Remove Quota Exceeded403 - Partner Endpoint Disabled403 - Authorization Error429 - Rate limited500 - Internal Server Error500 - Partial Internal Error

Updated over 2 years ago

---

Did this page help you?

Yes

No