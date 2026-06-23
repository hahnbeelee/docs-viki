# Source: https://docs.developer.yelp.com/reference/oauth2_revoke

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the OAuth Authorization flow, visit [OAuth Authorization](https://docs.developer.yelp.com/docs/oauth-authorization) to learn more.

client\_id

string

required

ID assigned by Yelp for the third-party system that will make user-authorized requests to Yelp.

client\_secret

string

required

length between 64 and 64

Client secret assigned by Yelp for the third-party system that will make user-authorized requests to Yelp.

token

string

required

length between 128 and 128

The access token to revoke.

token\_type\_hint

string

enum

Token type identifier, optional.

access\_tokenrefresh\_token

Allowed:

`access_token``refresh_token`

# 

200

A successful request doesn't return anything

# 

400

Bad Request

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

200400 - INVALID REQUEST400 - INVALID GRANT400 - UNSUPPORTED GRANT TYPE400 - BAD CLIENT ID OR SECRET400 - UNAUTHORIZED CLIENT429 - Rate limited500 - Internal Server Error

Updated over 2 years ago

---