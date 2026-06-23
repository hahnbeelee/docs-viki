# Source: https://docs.developer.yelp.com/docs/business-subscriptions-migration-guide

> ## 👍
> 
> Important Note
> 
> All existing subscriptions will still remain and can already be retrieved and managed using the Business Subscriptions API. Data between versions for the API are kept in sync.

## 

Overview

This Migration Guide will go through all the steps necessary to migrate from using any of the [Location Subscriptions v1](https://docs.developer.yelp.com/reference/testinput), [Location Subscriptions v2](https://docs.developer.yelp.com/reference/add_business_subscriptions_v2), [Listing Management](https://docs.developer.yelp.com/reference/get_listing_management_subscriptions_v1) or [Webhooks](https://docs.developer.yelp.com/reference/add_businesses_to_allow_list) APIs to the generic [Business Subscriptions API](https://docs.developer.yelp.com/docs/business-subscriptions-api)

## 

Changelog

- New endpoints
 - Can now update multiple subscription types within one request.
 - Webhook subscriptions can now be retrieved.
- All create/remove requests run asynchronously. A successful request implies, that a job has been created that will start to add/remove subscriptions. This job can't be awaited.
- Error messages share the same schema.

## 

Please see the specific migration guides

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Location Subscriptions](https://docs.developer.yelp.com/docs/location-subscriptions)

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Listing Management Migration Guide](https://docs.developer.yelp.com/docs/listing-management-migration-guide)

[![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Webhook Subscriptions Migration Guide](https://docs.developer.yelp.com/docs/webhook-subscriptions-migration-guide)

Copy Page