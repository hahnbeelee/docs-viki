# Source: https://docs.developer.yelp.com/docs/listing-management-migration-guide

> ## 👍
> 
> Important Note
> 
> All existing subscriptions will still remain and can already be retrieved and managed using the Business Subscriptions API. Data between both APIs is kept in sync.

## 

Migration Steps

1. Reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) to help you get started with your Yelp Fusion App. If you're already using other Yelp Fusion APIs you might be able to reuse that App.
2. Follow the changelog below to adjust your application

## 

Changes

- New authentication method
- New endpoint urls, different request schemas, same response schemas.
- Improved error case documentation

## 

New endpoints

The Business Subscriptions API exposes new URLs and expects new request schemas. To continue retrieving/creating/removing Listing Management Subscriptions, the following changes have to be made. 
See [Business Subscriptions API Reference](https://docs.developer.yelp.com/reference/get_business_subscriptions) for more details about the new endpoints.

### 

Get subscriptions

**Old**: `GET https://partner-api.yelp.com/listing_management/businesses/v1` 
**New**: `GET https://api.yelp.com/v3/businesses/subscriptions?subscription_type=LISTING_MANAGEMENT`

#### 

Notes

- Specify subscription\_type in url.
- Response additionally includes `subscription_type`, retains all other fields.

### 

Create new subscriptions

**Old**:

`POST https://partner-api.yelp.com/listing_management/businesses/add/v1 Body: {     "business_ids": ["bzRqPKp63X0u6fUtbg"] } Response code: 204`

**New**:

`POST https://api.yelp.com/v3/businesses/subscriptions {     "subscription_types": ["LISTING_MANAGEMENT"],     "business_ids": ["bzRqPKp63X0u6fUtbg"] } Response code: 202`

#### 

Notes

- Specify subscription\_types for which to subscribe in body.
- Successful response code changed from 204 to 202.

### 

Remove subscriptions

**Old**:

`POST https://partner-api.yelp.com/listing_management/businesses/remove/v1 {     "business_ids": ["VXi7gzRqPKp63X0u6fUtbg"]  } Response code: 204`

**New**:

`DELETE https://api.yelp.com/v3/businesses/subscriptions {     "subscription_types": ["LISTING_MANAGEMENT"]     "business_ids": ["VXi7gzRqPKp63X0u6fUtbg"]  } Response code: 202`

#### 

Notes

- Specify subscription\_types for which to subscribe in body.
- Successful response code changed from 204 to 202.
- HTTP Method changed from `POST` to `DELETE`.

## 

New authentication method

Authentication was simplified and is now using a [Yelp Fusion App](https://www.yelp.com/developers/documentation/v3/authentication).

> ## 📘
> 
> Set up required.
> 
> Please reach out to [partner-support@yelp.com](mailto:partner-support@yelp.com) to get your Fusion App set up for access to Business Subscriptions API.

| Old | New |
| --- | --- |
| Username and password | API Key |
| Changing credentials is full serve | Refresh your API Key yourself on [Yelp](https://www.yelp.com/developers/v3/manage_app) |
| Getting credentials requires emailing Yelp a PGP Key and receiving an encrypted email | View your API Key yourself on [Yelp](https://www.yelp.com/developers/v3/manage_app) |

[Click here for all details of Yelp Fusion Authentication](https://www.yelp.com/developers/documentation/v3/authentication)

## 

Errors

- renamed `id` to `code` for consistency with other Yelp API errors
- Improved documentation to clarify what kind of http statuses and error codes are expected in particular scenarios

### 

Example

Instead of

JSON

`HTTP Status Code: 413 {   "error": {     "id": "ERROR_ID",     "description": "The number of businesses in the request exceeded the maximum (500)",   } }`

the API will now return

JSON

`HTTP Status Code: 413 {   "error": {     "code": "ERROR_ID",     "description": "The number of businesses in the request exceeded the maximum (500)"   } }`

Updated over 3 years ago

---

Did this page help you?

Yes

No

Copy Page