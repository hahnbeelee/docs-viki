# Source: https://docs.developer.yelp.com/docs/webhook-subscriptions-migration-guide

> ## 👍
> 
> Important Note
> 
> All existing subscriptions will still remain and can already be retrieved and managed using the Business Subscriptions API. Data between both APIs is kept in sync.

## 

Migration Steps

If you're already using the existing webhooks APIs no set up is required, simply follow the changelog below and call the new endpoints.

## 

Changelog

- New endpoint to retrieve webhook subscriptions
- New endpoints and request/response schemas

## 

New endpoints

> ## ❗️
> 
> Updates are now processed asynchronously
> 
> The create and delete requests are now processed asynchronously. A successful request implies, that a job has been created that will start to create or delete webhook subscriptions. This job can't be awaited.

### 

NEW: Get subscriptions

With the Business Subscriptions API you are now able to retrieve your Webhook Subscriptions using the following endpoint ([API Reference](https://docs.developer.yelp.com/reference/get_business_subscriptions)):

`GET https://api.yelp.com/v3/businesses/subscriptions?subscription_type=WEBHOOK`

### 

Create subscriptions

**Old**:

`POST https://api.yelp.com/v3/webhooks/whitelists/businesses/add {     "business_ids": ["bzRqPKp63X0u6fUtbg"] }  Response status: 200 Response body: {“whitelist_business_ids_count”: 2}`

**New**:

`POST https://api.yelp.com/v3/businesses/subscriptions {     "subscription_types": ["WEBHOOK"],     "business_ids": ["bzRqPKp63X0u6fUtbg"] } Response status: 202 - Accepted Response body: {}`

#### 

Notes

- Specify the `subscription_type` in the body.
- Response status changed from 200 to 202.
- The `whitelist_business_ids_count` has been removed as updates are processed asynchronously. Use the [get\_business\_subscriptions](https://docs.developer.yelp.com/reference/get_business_subscriptions) to get the total count.

### 

Remove subscriptions

**Old**:

`POST https://api.yelp.com/v3/webhooks/whitelists/businesses/remove {     "business_ids": ["VXi7gzRqPKp63X0u6fUtbg"]  } Response status: 200 Response body: {“whitelist_business_ids_count”: 0}`

**New**:

`DELETE https://api.yelp.com/v3/businesses/subscriptions {     "subscription_types": ["WEBHOOK"]     "business_ids": ["VXi7gzRqPKp63X0u6fUtbg"]  } Response status: 202 - Accepted Response body: {}`

#### 

Notes

- Specify the `subscription_type` in the body.
- Response status changed from 200 to 202.
- The `whitelist_business_ids_count` has been removed as updates are processed asynchronously. Use the [get\_business\_subscriptions](https://docs.developer.yelp.com/reference/get_business_subscriptions) to get the total count.

Updated over 3 years ago

---

Did this page help you?

Yes

No

Copy Page