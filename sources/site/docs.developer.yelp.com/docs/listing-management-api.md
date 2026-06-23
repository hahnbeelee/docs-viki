# Source: https://docs.developer.yelp.com/docs/listing-management-api

> ## 🚧
> 
> Listing Management Subscription API is deprecated
> 
> Please migrate to the [Business Subscriptions API](https://docs.developer.yelp.com/docs/business-subscriptions-api)

# 

Overview

TBD

# 

Authentication

Authentication uses basic HTTP authentication over SSL. The Data Ingestion API credentials are required to make calls to these endpoints. To gain access to these endpoints, please email [partner-support@yelp.com](mailto:partner-support@yelp.com)

# 

Endpoints

## 

GET /listing\_management/businesses/v1

This endpoint returns a paginated list of active business subscriptions for Listing Management.

**Request Query Parameters**

| Field name | Field description |
| --- | --- |
| `limit` | Number of business subscriptions to return per page. 
 
Default: 50 
Minimum: 1 
Maximum: 10 000 |
| `offset` | Page offset. 
 
Default: 0 |

Example Request (Shell)

`curl -X GET \      --user "<user>:<password>" \      "https://partner-api.yelp.com/listing_management/businesses/v1?limit=2&offset=0"`

**Response Body Parameters**

| Field name | Field description |
| --- | --- |
| `limit` | Current limit |
| `offset` | Current page offset |
| `total` | Total number of business subscriptions |
| `subscriptions` | List of business subscriptions |
| `subscriptions[].business_id` | Business ID |
| `subscriptions[].subscribed_at` | ISO 8601 formatted datetime in UTC of when the subscription started. 
 
Example: 2020-02-21T10:40:50+00:00 |

Example Response (JSON)

`{   "total": 3,   "limit": 2,   "offset": 0,   "subscriptions": [     {       "subscribed_at": "2020-02-21T10:40:50+00:00",       "business_id": "VUMc8yNaIW7E3K19nabXfA"     },     {       "subscribed_at": "2020-02-21T10:43:11+00:00",       "business_id": "bOEsE8ZSp6ltTKB9deFeYw"     }   ] }`

## 

POST /listing\_management/businesses/add/v1

This endpoint creates new business subscriptions for Listing Management.

**Request Body Parameters**

| Field name | Field description |
| --- | --- |
| `business_ids` | List of Business IDs 
 
Minimum: 1 
Maximum: 500 |

Example Request (Shell)

`curl -H "Content-Type: application/json" \      --user "<user>:<password>" \      -X POST \      -d '{"business_ids": ["etdmKzPCEQSBQo4CTRRnDv", "1z5LeXsmSC8TS3yAGFaHZw"]}' \      "https://partner-api.yelp.com/listing_management/businesses/add/v1"`

**Response Body Parameters**

N/A

Example Response (JSON)

`{}`

## 

POST /listing\_management/businesses/remove/v1

This endpoint deletes business subscriptions for Listing Management.

**Request Body Parameters**

| Field name | Field description |
| --- | --- |
| `business_ids` | List of Business IDs 
 
Minimum: 1 
Maximum: 500 |

Example Request (Shell)

`curl -H "Content-Type: application/json" \      --user "<user>:<password>" \      -X POST \      -d '{"business_ids": ["etdmKzPCEQSBQo4CTRRnDv", "1z5LeXsmSC8TS3yAGFaHZw"]}' \      "https://partner-api.yelp.com/listing_management/businesses/remove/v1"`

**Response Body Parameters**

N/A

Example Response (JSON)

`{}`

> ## 📘
> 
> Check out our Listing Management API Reference Page
> 
> ![:owlbert:](https://docs.developer.yelp.com/public/img/emojis/owlbert.png) [Listing Management Endpoints](https://docs.developer.yelp.com/reference/retrieve-subscriptions)

Copy Page