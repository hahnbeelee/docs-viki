# Source: https://docs.developer.yelp.com/docs/graphql-rate-limiting

In addition to [QPS rate limiting](https://docs.developer.yelp.com/docs/fusion-qps-rate-limiting), there is also a limit to the amount of data that can be requested from the GraphQL API each day.

Rather than setting a limit on the number of GraphQL requests that can be made every 24 hours, Yelp's GraphQL API limits daily access based on how much data is returned. This makes sense because a single GraphQL call might return information about tens, hundreds or even thousands of Yelp businesses depending on how the query is constructed.

You can see your usage stats and how close you are to the daily limit on the [Manage App](https://www.yelp.com/developers/v3/manage_app) page.

Each object returned in a GraphQL response, such as a business or a review has a "points" value associated with it.

| Node Type | Points Value |
| --- | --- |
| businesses | 1 |
| business | 10 |
| business\_attributes | 1 |
| business\_attribute | 2 |
| reviews | 1 |
| review | 5 |
| event | 1 |
| user | 1 |
| location | 5 |
| coordinates | 1 |
| category | 1 |

> ## 📘
> 
> Please note
> 
> The points values per node are subject to change as we iterate and improve upon this system.

The points value of a particular node is the same regardless of how many fields within it are queried. For example, a business node is worth 1 point if the only field requested is 'name'. It is still worth 1 point if both the 'name' and 'rating' fields are requested.

Every 24-hour period each user has a limit of 25,000 points worth of data that they can obtain via Yelp's GraphQL API. This resets at midnight GMT. Some examples will assist in explaining how this system works.

## 

Daily Points Limit Examples

### 

Example 1

A query to get some basic business info and reviews about Yelp's headquarters.

GraphQL

`{     business(id: "yelp-san-francisco") {         name         id         alias         reviews {             rating             text         }     } }`

Let's say we get back the response body:

JSON

`{     "data": {         "business": {             "name": "Yelp",             "id": "4kMBvIEWPxWkWKFN__8SxQ",             "alias": "yelp-san-francisco",             "reviews": [                 {                     "rating": 5,                     "text": "..."                 },                 {                     "rating": 2,                     "text": "..."                 },                 {                     "rating": 5,                     "text": "..."                 }             ]         }     } }`

The above response has the following nodes:

- 1 business node worth 10 points
- 3 review nodes worth 5 points each

Which means that this query counts for 10+3\*5=25 points against the total daily points limit.

### 

Example 2

A query to search for the term 'burrito' in San Francisco, returning at most 2 businesses. For each business, get the name, rating, location and 1 review. For that one review, get the review text, rating and the display name of the review author.

GraphQL

`{     search(term: "burrito", location: "san francisco" limit: 2) {         total             business {                 name                 rating                 location {                     address1                     city                     state                     country                 }             reviews(limit: 1) {                 text                 rating                 user {                     name                 }             }         }     } }`

Let's say we get back the response body:

JSON

`{     "data": {         "search": {             "total": 1997,             "business": [                 {                     "name": "El Farolito",                     "rating": 4.0,                     "location": {                         "address1": "2779 Mission St",                         "city": "San Francisco",                         "state": "CA",                         "country": "US"                     },                     "reviews": [                         {                             "text": "...",                             "rating": 5,                             "user": {                                 "name": "Leslie H."                             }                         }                     ]                 },                 {                     "name": "La Taqueria",                     "rating": 4.0,                     "location": {                         "address1": "2889 Mission St",                         "city": "San Francisco",                         "state": "CA",                         "country": "US"                     },                     "reviews": [                         {                             "text": "...",                             "rating": 5,                             "user": {                                 "name": "Brenda A."                             }                         }                     ]                 }             ]         }     } }`

The above response has the following nodes:

- 1 businesses node (this is the node that contains the list of business objects) worth 1 points each
- 2 business nodes worth 10 points each
- 2 location nodes worth 5 points each
- 2 review nodes worth 5 points each
- 2 user nodes worth 1 point each

Which means that this query counts for 1 + 2\_10 + 2\_5 + 2\_5 +2\_1 = 43 points against the total daily points limit.

## 

When the Limit is Hit

If a user makes a GraphQL query after having reached their daily points limit, you will get back a response with only 'errors' set:

JSON

`{     "errors": [         {             "message": "You have reached the GraphQL daily points limit for this API key. The limit will reset at midnight GMT.",             "extensions": {                 "code": "DAILY_POINTS_LIMIT_REACHED"             }         }     ] }`

Copy Page