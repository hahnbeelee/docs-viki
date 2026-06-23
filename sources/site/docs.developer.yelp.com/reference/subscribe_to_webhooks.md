# Source: https://docs.developer.yelp.com/reference/subscribe_to_webhooks

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

webhook\_url

uri

required

The URL to which the webhook events will be sent.

webhook\_type

string

enum

required

The type of webhook event to subscribe to.

leads\_event

Allowed:

`leads_event`

restricted\_business\_ids

array of strings

length ≤ 50

An optional list of business IDs to restrict the webhook subscription to. If not provided, the webhook will be subscribed to events for all businesses the Biz Owner has access to. 
The maximum limit is 50 items.

restricted\_business\_ids

ADD string

# 

200

200 OK - Webhook successfully subscribed

# 

400

Bad Request

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

409

Conflict

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated 11 months ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200400 - Invalid Client ID400 - One or more business IDs were invalid400 - Exactly zero businesses are not allowed400 - More than the maximum number (100) of businesses is not allowed401 - Unauthorized401 - Invalid Token409 - Conflict429 - Rate limited500 - Internal Server Error

Updated 11 months ago

---