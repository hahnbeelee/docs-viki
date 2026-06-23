# Source: https://docs.developer.yelp.com/reference/redeem_authorization_code_for_access_token

⚠️

This reference guide is currently experiencing difficulties and will be back online shortly. Please contact [support@readme.io](mailto:support@readme.io?subject=API Explorer Error [ERR-YR5GEB]) with your error code.

`ERR-YR5GEB`

> ## 📘
> 
> This endpoint is part of the Respond to Reviews API, visit [Respond to Reviews API](https://docs.developer.yelp.com/docs/respond-to-reviews-api-v2) to learn more.

client\_id

string

required

ID assigned by Yelp for the third-party system that will make user-authorized requests to Yelp.

client\_secret

string

required

Client secret assigned by Yelp for the third-party system that will make user-authorized requests to Yelp.

code

string

required

A unique code that will be used by the client to redeem an access token.

grant\_type

string

required

The grant being presented in order to exchange for an access token. For example, when redeeming the authorization code for an access token, this value will be authorization\_code.

redirect\_uri

string

The client-provided redirect endpoint URL. If no redirect\_uri was provided during authorization, it is optional here.

# 

200

Successfully redeemed the authorization code for an access token.

# 

400

This error is returned in any of the following scenarios:

| id | Description | http\_code |
| --- | --- | --- |
| INVALID\_REQUEST | Missing a required parameter or includes an unsupported parameter. | HTTPBadRequest (400) |
| INVALID\_GRANT | The provided authorization grant is invalid, expired or revoked. | HTTPBadRequest (400) |
| UNAUTHORIZED\_CLIENT | The authenticated client is not authorized to use this authorization grant type. | HTTPBadRequest (400) |
| UNSUPPORTED\_GRANT\_TYPE | The authorization grant type is not supported by the authorization server. | HTTPBadRequest (400) |

# 

401

This error is returned in any of the following scenarios:

| id | Description | http\_code |
| --- | --- | --- |
| INVALID\_CLIENT | Client authentication failed due to unknown client, no client authentication included, or unsupported authentication method. | HTTPUnauthorized (401) |

# 

404

This error is returned in any of the following scenarios:

| id | Description | http\_code |
| --- | --- | --- |
| CLIENT\_NOT\_FOUND | Supplied client ID does not exist. | HTTPNotFound (404) |

Updated over 2 years ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

xxxxxxxxxx

1

curl \--request POST \\

2

 \--url https://partner-api.yelp.com/token/v1 \\

3

 \--header 'accept: application/json' \\

4

 \--header 'content-type: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Result400 - Invalid Request401 - Invalid Client404 - Client Not Found

Updated over 2 years ago

---

Did this page help you?

Yes

No