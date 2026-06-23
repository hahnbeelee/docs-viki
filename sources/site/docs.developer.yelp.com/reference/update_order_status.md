# Source: https://docs.developer.yelp.com/reference/update_order_status

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the Checkout API, visit [Checkout API](https://docs.developer.yelp.com/docs/checkout-api) to learn more.

yelp\_order\_id

string

required

ID of order that Yelp will try to update.

confirmation\_type

object

required

[ConfirmationType](https://docs.developer.yelp.com/docs/resources#confirmationtype-enum) enum. The state the order is being updated to.

confirmation\_type object

eta\_in\_minutes

integer

required

The estimated time of arrival.

# 

200

Successfully updated the order status.

# 

403

This error is returned in any of the following scenarios:

| Status | error\_code | error\_message (example) |
| --- | --- | --- |
| 403 | ORDER\_STATE\_INVALID | Order is in an invalid state to perform this operation. |

Updated over 2 years ago

---

ShellNodeRubyPHPPython

:

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result

Updated over 2 years ago

---