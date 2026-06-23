# Source: https://docs.developer.yelp.com/reference/remove_businesses_to_allow_list

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 🚧
> 
> Webhooks API is deprecated
> 
> Please migrate to the [Business Subscriptions API](https://docs.developer.yelp.com/docs/business-subscriptions-api)

business\_ids

array of strings

required

length between 1 and 100

A list of Yelp Business IDs

business\_ids\*

string

Yelp Business IDs

ADD string

# 

200

200

# 

400

Bad Request

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

404

You are not signed up to use this service.

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated over 2 years ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Client ID400 - One or more business IDs were invalid400 - Exactly zero businesses are not allowed400 - More than the maximum number (100) of businesses is not allowed401 - Unauthorized401 - Invalid Token404 - Result429 - Rate limited500 - Internal Server Error

Updated over 2 years ago

---