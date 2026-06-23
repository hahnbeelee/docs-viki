# Source: https://docs.developer.yelp.com/reference/get_business_subscriptions_v2

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 🚧
> 
> Location Subscription API is deprecated
> 
> Please migrate to the [Business Subscriptions API](https://docs.developer.yelp.com/docs/business-subscriptions-api)

Get the List of businesses included in the Partners' Feed.

## 

200 Success Response Schema

| Field Name | Field Type | Field Description |
| --- | --- | --- |
| `total` | `integer` | Total number of businesses subscribed to for the Partners' Feed. |
| `offset` | `integer` | Current offset. |
| `limit` | `integer` | Current limit. |
| `subscriptions` | `list` | List of businesses subscribed to for the Partners' Feed. |
| `subscriptions.business_id` | `string` | Business identifier. |
| `subscriptions.subscribed_at` | `string` | Time when the subscription started. |

limit

int32

Defaults to 100

Number of business IDs returned on this request, maximum 10 000, minimum 1.

offset

int32

Defaults to 0

Position of first business ID returned on this request, minimum 0.

# 

200

200

Updated over 3 years ago

---

Shell

Bearer

Loading…

Choose an example:

application/json

200 - Result

Updated over 3 years ago

---