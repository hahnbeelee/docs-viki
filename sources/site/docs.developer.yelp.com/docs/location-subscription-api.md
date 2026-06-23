# Source: https://docs.developer.yelp.com/docs/location-subscription-api

> ## 🚧
> 
> Location Subscription API is deprecated
> 
> Please migrate to the [Business Subscriptions API](https://docs.developer.yelp.com/docs/business-subscriptions-api)

> ## ❗️
> 
> Deprecated Version
> 
> This page describes the deprecated v1 Version of the Location Subscription API. It's deprecated and will be removed in the future.
> 
> Please start migrating your clients to use the new version. [New Location Subscription API v2 Docs](https://docs.developer.yelp.com/docs/location-subscription-api-v2)

# 

Overview

Location Subscription is the system that generates data on Yelp businesses and stores it on Amazon S3 buckets. Partners can use the Location Subscription API to modify the list of businesses that appear in their subscription feed. The API has add, remove, list, and quota endpoints.

# 

Authentication

Authentication uses basic HTTP authentication over SSL. Credentials are provided separately.

# 

Endpoints

## 

POST /syndication/feed/add

This endpoint is used to add business IDs to the subscription list. The post accepts a JSON list of business IDs mapped to the key 'biz\_ids'.

**Request Body Parameters**

| Field Name | Field Description |
| --- | --- |
| `biz_ids` | list of encrypted business IDs to add to the daily subscription feed. This endpoint support max 1000 business IDs per query. |

Example Request (Shell)

`curl -H "Content-Type: application/json" \      -X POST \      -d '{"biz_ids":["bzRqPKp63X0u6fUtbg"]}' \      --user "<user>:<password>" \      "https://partner-api.yelp.com/syndication/feed/add"`

**Response Body Parameters**

| Field Name | Field Description |
| --- | --- |
| `new` | new IDs that were inserted into the database |
| `reactivated` | IDs that were disabled and are now re-enabled |
| `already_active` | IDs that were already active in this query |

Example Response (JSON)

`{   "new": [],    "reactivated": [],    "already_active": [] }`

## 

POST /syndication/feed/remove

This endpoint is used to disable business IDs from the subscription list. The post accepts a list of business IDs mapped to the key "biz\_ids". 
**Response Body Parameters**

| Field Name | Field Description |
| --- | --- |
| `biz_ids` | list of business IDs to add to the daily subscription feed |

Example Request (Shell)

`curl -H "Content-Type: application/json" \      -X POST \      -d '{"biz_ids":["VXi7gzRqPKp63X0u6fUtbg"]}' \      --user "<user>:<password>" \      "https://partner-api.yelp.com/syndication/feed/remove"`

**Response Params**

| Field Name | Field Description |
| --- | --- |
| `status` | Status of disabling business IDs |

Example Response (JSON)

`{   "status": "completed" }`

## 

GET /syndication/feed/quota

This endpoint is gets quota information. Takes in no parameters.

**Request Params** 
None

Example Request (Shell)

`curl -X GET \      -H "Accept: application/json" \      -H "Content-type: application/json" \      --user "<user>:<password>" \      "https://partner-api.yelp.com/syndication/feed/quota"`

**Response Params**

| Field Name | Field Description |
| --- | --- |
| `number_of_active_businesses` | number of currently active businesses |

Example Response (JSON)

`{   "number_of_active_businesses": 17 }`

## 

GET /syndication/feed/list

This endpoint is used to get the list of subscription business IDs. The two query params have default values of 0.

**Request Query Parameters**

| | |
| --- | --- |
| `limit` | number of business IDs returned on this request, maximum 1000 |
| `offset` | position of first business ID returned on this request, minimum 0 |

Example Request (Shell)

`curl -X GET \      -H "Accept: application/json" \      -H "Content-type: application/json" \      --user "<user>:<password>" \      "https://partner-api.yelp.com/syndication/feed/list?limit=1&offset=1"`

**Response Parameters**

| Field Name | Field Description |
| --- | --- |
| `biz_id` | list of business IDs returned by this query |

Example Response (JSON)

`{   "biz_ids": ["VXi7gzRqPKp63X0u6fUtbg"] }`

# 

Error Codes

| Error Name | Error Description |
| --- | --- |
| `ADDITION_EXCEEDS_BIZ_QUOTA` | The new additions would exceed the business quota. |
| `BAD_POST_BODY` | A list mapped to the key "biz\_ids" is required in the request body. |
| `BIZ_ID_LIST_TOO_LARGE` | The biz id list is larger than the maximum size of 1000. |
| `INVALID_LIMIT_VALUE` | The limit must be greater than 0 and less or equal to 10000. |
| `INVALID_JSON_OBJECT` | The request body could not be parsed into a JSON object. |
| `INVALID_OFFSET_VALUE` | The offset must be greater or equal to 0. |
| `INVALID_QUERY_PARAM_TYPE` | Query parameters must be of type integer. |
| `INVALID_IDS_IN_POST_BODY` | The post body contains invalid business IDs. |
| `REMOVE_EXCEEDS_LIMIT` | The remove call exceeds the yearly remove limit. |

**Response Params**

| Field Name | Field Description |
| --- | --- |
| `error` | error object generated by this request |
| `error.message` | message describing the error |
| `error.code` | error code associated with this error |
| `error.invalid_ids` | invalid IDs in the post body (used for add/remove endpoints) |

Example Response (JSON)

`{   "error": {     "message": "The post body contains invalid business ids",      "code": "INVALID_IDS_IN_POST_BODY",     "invalid_ids": ["VXi7gzRqPKp63X0"]    } }`

Updated over 3 years ago

---

Did this page help you?

Yes

No

Copy Page