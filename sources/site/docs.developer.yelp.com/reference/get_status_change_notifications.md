# Source: https://docs.developer.yelp.com/reference/get_status_change_notifications

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
> This endpoint is part of the Checkout API, visit [Checkout API](https://docs.developer.yelp.com/docs/checkout-api) to learn more.

yelp\_order\_id

string

required

ID of order that Yelp will try to update.

offset

integer

Defaults to 0

Pagination offset

limit

integer

1 to 100

Defaults to 100

Pagination limit

# 

200

Successfully retrieved order status notifications.

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

 \--url 'https://partner-api.yelp.com/checkout/orders/yelp\_order\_id/notifications/v3?offset=0&limit=100' \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result

Updated over 2 years ago

---

Did this page help you?

Yes

No