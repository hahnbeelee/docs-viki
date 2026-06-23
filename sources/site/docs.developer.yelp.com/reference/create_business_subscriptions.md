# Source: https://docs.developer.yelp.com/reference/create_business_subscriptions

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

subscription\_types

array of objects

required

Types of subscriptions that will be managed

subscription\_types\*

Allowed:

`LISTING_MANAGEMENT``YELP_KNOWLEDGE``WEBHOOK`

ADD string

business\_ids

array of strings

required

length between 1 and 1000

List of Yelp Encrypted Business IDs that will be managed.

business\_ids\*

string

Yelp Encrypted Business ID.

ADD string

# 

202

Request accepted. The business subscriptions will be created asynchronously

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
- The monthly create quota for YELP\_KNOWLEDGE subscriptions would be exceeded with the incoming request.

| code | description |
| --- | --- |
| PARTNER\_ENDPOINT\_DISABLED | You are trying to access a Partner API endpoint for which your API Client has not been enabled. Please reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) for more information. |
| AUTHORIZATION\_ERROR | Authorization Error |
| QUOTA\_EXCEEDED | Exceeded the monthly create quota. |

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

curl \--request POST \\

2

 \--url https://api.yelp.com/v3/businesses/subscriptions \\

3

 \--header 'accept: application/json' \\

4

 \--header 'content-type: application/json' \\

5

 \--data '{"business\_ids":\[\]}'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

202400 - Invalid Request401 - Unauthorized401 - Invalid Token403 - Create Quota Exceeded403 - Partner Endpoint Disabled403 - Authorization Error429 - Rate limited500 - Internal Server Error500 - Partial Internal Error

Updated over 2 years ago

---

Did this page help you?

Yes

No