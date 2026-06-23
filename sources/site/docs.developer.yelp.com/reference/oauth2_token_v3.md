# Source: https://docs.developer.yelp.com/reference/oauth2_token_v3

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the OAuth Authorization flow, visit [OAuth Authorization](https://docs.developer.yelp.com/docs/oauth-authorization) to learn more.

Access Token RequestRefresh Access Token Request

Access Token Request as per [https://www.rfc-editor.org/rfc/rfc6749#section-4.1.3](https://www.rfc-editor.org/rfc/rfc6749#section-4.1.3)

client\_id

string

required

ID assigned by Yelp for the third-party system that will make user-authorized requests to Yelp.

client\_secret

string

required

length between 64 and 64

Client secret assigned by Yelp for the third-party system that will make user-authorized requests to Yelp.

grant\_type

string

enum

required

Value MUST be set to "authorization\_code".

authorization\_code

Allowed:

`authorization_code`

code

string

required

Authorization code that is sent back to the redirect uri after a biz user authorized the client's oauth client.

redirect\_uri

string

REQUIRED, if the "redirect\_uri" parameter was included in the authorization request and their values MUST be identical.

# 

200

Token issued

# 

400

Bad Request

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated over 1 year ago

---

ShellNodeRubyPHPPython

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Authorization Code Example200 - Refresh Token Example400 - INVALID REQUEST400 - INVALID GRANT400 - UNSUPPORTED GRANT TYPE400 - BAD CLIENT ID OR SECRET400 - UNAUTHORIZED CLIENT429 - Rate limited500 - Internal Server Error

Updated over 1 year ago

---