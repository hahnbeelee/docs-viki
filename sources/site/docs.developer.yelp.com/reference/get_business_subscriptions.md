# Source: https://docs.developer.yelp.com/reference/get_business_subscriptions

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the Business Subscriptions API, visit [Business Subscriptions API](https://docs.developer.yelp.com/docs/business-subscriptions-api) to learn more.

subscription\_type

string

enum

required

Type of subscriptions being returned

LISTING\_MANAGEMENTYELP\_KNOWLEDGEWEBHOOK

Allowed:

`LISTING_MANAGEMENT``YELP_KNOWLEDGE``WEBHOOK`

limit

integer

0 to 10000

Defaults to 100

The maximum number of business subscriptions to return.

offset

integer

≥ 0

Defaults to 0

Offset the list of returned business subscriptions by this amount.

# 

200

Successfully fetched the business subscriptions

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

| code | description |
| --- | --- |
| PARTNER\_ENDPOINT\_DISABLED | You are trying to access a Partner API endpoint for which your API Client has not been enabled. Please reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) for more information. |
| AUTHORIZATION\_ERROR | Authorization Error |

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

200 - Result400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Partner Endpoint Disabled403 - Authorization Error429 - Rate limited500 - Internal Server Error

Updated over 2 years ago

---