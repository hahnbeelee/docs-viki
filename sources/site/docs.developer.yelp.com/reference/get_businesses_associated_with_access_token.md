# Source: https://docs.developer.yelp.com/reference/get_businesses_associated_with_access_token

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the Respond to Reviews API, visit [Respond to Reviews API](https://docs.developer.yelp.com/docs/respond-to-reviews-api-v2) to learn more.

# 

200

Successfully retrieved the businesses.

# 

400

This error is returned in any of the following scenarios:

| id | Description | http\_code |
| --- | --- | --- |
| INVALID\_REQUEST | Missing a required parameter or includes an unsupported parameter. | HTTPBadRequest (400) |
| INSUFFICIENT\_SCOPE | The request requires higher privileges than provided by the access token. | HTTPBadRequest (400) |

# 

401

This error is returned in any of the following scenarios:

| id | Description | http\_code |
| --- | --- | --- |
| INVALID\_TOKEN | The access token provided is expired, revoked, malformed, or invalid for other reasons | HTTPUnauthorized (401) |

Updated over 2 years ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Request400 - Insufficient Scope401 - Invalid Token

Updated over 2 years ago

---