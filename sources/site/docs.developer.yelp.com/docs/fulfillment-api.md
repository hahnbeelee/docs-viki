# Source: https://docs.developer.yelp.com/docs/fulfillment-api

> ## 📘
> 
> This is a Yelp Partner API
> 
> Access is disabled by default. See [Yelp Partner APIs](https://docs.developer.yelp.com/docs/yelp-partner-apis) on how to get access.

# 

If you are upgrading from v1 APIs

- the request is now a formal Opportunity resource
- request now has `service_type`, `selected_option`, and `availability_constraints`
- all "delivery"-specific wording is now generally `at_customer`
- `fulfillment_address` is now `address_constraint` (just a string)
- partner needs to send us address suggestions when relevant
- \[2014-8-12\] Added RepeatOrderConstraint and expectations from the partner iframe when showing a re-order.
- \[2014-8-12\] Provided a recommended precedence order for checking multiple availability constraints.
- \[2014-8-12\] Added 2 more enums to AvailabilityStatus enum to handle repeat orders.
- \[2015-3-1\] Added a `customer_address` dict to the `CustomerAddressConstraint` resource

Updated over 3 years ago

---

Did this page help you?

Yes

No

Copy Page