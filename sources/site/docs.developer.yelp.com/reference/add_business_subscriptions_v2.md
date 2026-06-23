# Source: https://docs.developer.yelp.com/reference/add_business_subscriptions_v2

> ## 🚧
> 
> Location Subscription API is deprecated
> 
> Please migrate to the [Business Subscriptions API](https://docs.developer.yelp.com/docs/business-subscriptions-api)

Subscribe businesses to the Partners' Feed.

business\_ids

array of strings

List of encrypted business IDs to subscribe to the Partners' Syndication Feed. Minimum of 1 ID, maximum of 1000 IDs per request. Requires IDs to be unique within the array.

business\_ids

ADD string

# 

202

202

# 

400

400

Updated over 3 years ago

---

Did this page help you?

Yes

No

Shell

Bearer

xxxxxxxxxx

1

curl \-X POST \\

2

 \-H "Content-Type: application/json" \\

3

 \-d '{"business\_ids":\["bzRqPKp63X0u6fUtbg"\]}' \\

4

 \--user "<user>:<password>" \\

5

 "https://partner-api.yelp.com/syndication/businesses/add/v2"

Choose an example:

application/json

202 - Result400 - Result

Updated over 3 years ago

---

Did this page help you?

Yes

No