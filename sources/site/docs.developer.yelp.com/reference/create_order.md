# Source: https://docs.developer.yelp.com/reference/create_order

⚠️

This reference guide is currently experiencing difficulties and will be back online shortly. Please contact [support@readme.io](mailto:support@readme.io?subject=API Explorer Error [ERR-YR5GEB]) with your error code.

`ERR-YR5GEB`

> ## 📘
> 
> This endpoint is part of the Checkout API, visit [Checkout API](https://docs.developer.yelp.com/docs/checkout-api) to learn more.

order

object

See [Order Resource](https://docs.developer.yelp.com/docs/resources#section-order)

order object

notification\_url

string

required

HTTPS URL to which Yelp shall POST OrderStatus updates - e.g. when charge processing is completed

opportunity\_id

string

required

token that Yelp passed to partner via iframe and when checking availability of business

# 

200

Successfully created an order.

# 

400

This error is returned in any of the following scenarios:

| Status | error\_code | error\_message (example) |
| --- | --- | --- |
| 400 | UNREGISTERED\_PARTNER\_BUSINESS\_ID | The partner business id specified is not mapped to a known Yelp business id |

# 

403

This error is returned in any of the following scenarios:

| Status | error\_code | error\_message (example) |
| --- | --- | --- |
| 403 | UNAUTHORIZED | Partner is not enabled for V3 API flow |

# 

412

This error is returned in any of the following scenarios:

| Status | error\_code | error\_message (example) |
| --- | --- | --- |
| 412 | CURRENCY\_MISMATCH\_ERROR | Currency mismatch with partner contract |

Updated over 2 years ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

:

xxxxxxxxxx

1

curl \--request POST \\

2

 \--url https://partner-api.yelp.com/checkout/orders/create/v3 \\

3

 \--header 'accept: application/json' \\

4

 \--header 'content-type: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400

Updated over 2 years ago

---

Did this page help you?

Yes

No