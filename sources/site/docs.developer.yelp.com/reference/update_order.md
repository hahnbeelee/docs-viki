# Source: https://docs.developer.yelp.com/reference/update_order

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

order

object

Current complete (not a diff) Order as it should be after updates. See [Order Resource](https://docs.developer.yelp.com/docs/resources#section-order)

order object

# 

200

Successfully started the asynchronous process of updating an order.

# 

403

This error is returned in any of the following scenarios:

| Status | error\_code | error\_message (example) |
| --- | --- | --- |
| 403 | UNAUTHORIZED | Partner is not enabled for V3 API flow |

# 

422

This error is returned in any of the following scenarios:

| Status | error\_code | error\_message (example) |
| --- | --- | --- |
| 422 | INVALID\_ORDER\_OPERATION | The order cannot be updated (either because it is cancelled or because another partner request is being processed) |
| 422 | COLLECTION\_TYPE\_MUST\_BE\_PREPAID | If the collection\_type is passed as something other than `prepaid` |

# 

423

This error is returned in any of the following scenarios:

| Status | error\_code | error\_message (example) |
| --- | --- | --- |
| 423 | ORDER\_NOT\_READY\_FOR\_OPERATION | Order is locked because another operation is in progress |

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