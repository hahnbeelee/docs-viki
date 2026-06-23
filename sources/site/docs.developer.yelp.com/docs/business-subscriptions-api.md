# Source: https://docs.developer.yelp.com/docs/business-subscriptions-api

> ## 📘
> 
> Migrating from an existing API?
> 
> Checkout the [Changelog and Migration Guide](https://docs.developer.yelp.com/docs/business-subscriptions-migration-guide)

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

## 

Overview

The Business Subscriptions API allows Yelp partners to manage their business subscriptions. Business subscriptions are managed separately per use case. Different subscription types can now be updated within one API call.

The subscriptions can have the following types that determine what they are used for:

- [Location Subscriptions](https://docs.developer.yelp.com/docs/location-subscription-api-v2) (subscription type `YELP_KNOWLEDGE`) 
 Subscribed businesses will be part of the generated partner feed.
 
- [Listing Management](https://docs.developer.yelp.com/docs/listing-management-api) (subscription type `LISTING_MANAGEMENT`) 
 Subscribed business's listing can be managed.
 
- [Webhooks](https://docs.developer.yelp.com/docs/webhooks) (subscription type `WEBHOOK`) 
 Receive real-time notifications about events triggered on the subscribed businesses.
 

### 

Requests are processed asynchronously

The add and delete endpoint requests are processed asynchronously. A successful response from these endpoints only represents the successful start of processing the request. It's not possible to await the actual adding or removing of business subscriptions. Expect 99% of requests to be processed within 15 minutes.

## 

Authentication

The API uses your Yelp Places Api Key for authentication. See [Yelp Places Authentication](https://docs.developer.yelp.com/docs/fusion-authentication) for details.

Your Yelp Places Client needs to be enabled for Business Subscriptions API. Please send your Client ID and the subscription types that you are going to manage to [partner-support@yelp.com](mailto:partner-support@yelp.com).

## 

Deprecation

The Business Subscriptions API replaces the [Location Subscriptions v1](https://docs.developer.yelp.com/reference/testinput), [Location Subscriptions v2](https://docs.developer.yelp.com/reference/add_business_subscriptions_v2), [Listing Management](https://docs.developer.yelp.com/reference/get_listing_management_subscriptions_v1) and [Webhooks](https://docs.developer.yelp.com/reference/add_businesses_to_allow_list) APIs. These APIs will no longer be supported after July 2023 and turned off January 2024. 
Instead of separating these subscriptions by endpoints, they are separated by type into this single API. Follow the Migration Guides to get started with the Business Subscriptions API if you used one of the just mentioned Subscriptions APIs before. Click on the API that you are currently using to get to the Migration Guide: [Location Subscription V1](https://docs.developer.yelp.com/docs/location-subscriptions), [Location Subscriptions V2](https://docs.developer.yelp.com/docs/location-subscriptions), [Listing Management](https://docs.developer.yelp.com/docs/listing-management-migration-guide), [Webhook](https://docs.developer.yelp.com/docs/webhook-subscriptions-migration-guide).

## 

Business IDs

The Business Subscriptions API requires Business IDs when managing subscriptions. Please reference the [Business Match API documentation](https://docs.developer.yelp.com/reference/v3_business_match) on how to get Business IDs for Yelp listings.

All the Business Subscriptions API endpoints have a default rate limit of 5 requests per second per client per endpoint. The limits are configurable for clients, contact us to know more. For more details, see [QPS Rate Limiting](https://docs.developer.yelp.com/docs/fusion-qps-rate-limiting)

## 

Endpoints

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Get Business Subscriptions](https://docs.developer.yelp.com/reference/get_business_subscriptions)

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Subscribe to businesses](https://docs.developer.yelp.com/reference/create_business_subscriptions)

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Unsubscribe from businesses](https://docs.developer.yelp.com/reference/remove_business_subscriptions)

Get your current quota information (this is only supported for subscriptions of type `YELP_KNOWLEDGE`):

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Get Quota](https://docs.developer.yelp.com/reference/get_business_subscriptions_quota)

Copy Page