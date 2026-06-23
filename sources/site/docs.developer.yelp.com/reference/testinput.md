# Source: https://docs.developer.yelp.com/reference/testinput

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

## 

200 Success Response Schema

| Field Name | Field Type | Field Description |
| --- | --- | --- |
| `new` | `list` | New IDs that were inserted into the database. |
| `reactivated` | `list` | IDs that were disabled and are now re-enabled. |
| `already_active` | `list` | IDs that were already active in this query. |

biz\_ids

array of strings

required

List of encrypted business IDs to add to the daily subscription feed. This endpoint support max 1000 business IDs per query.

biz\_ids\*

ADD string

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