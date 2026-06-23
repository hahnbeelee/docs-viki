# Source: https://docs.developer.yelp.com/docs/refresh-tokens

Refresh tokens are credentials used to obtain access tokens. For more information, see [RFC 6749](https://www.rfc-editor.org/rfc/rfc6749#section-1.5).

When you redeem an authorization code for an access token, a refresh token is issued, too. Refresh tokens are valid for 365 days by default, and access tokens are valid for 7 days; see [Token Lifetime](https://docs.developer.yelp.com/docs/authorization-code-workflow#token-lifetimes). After a refresh token expires, the user needs to reauthorize the application.

Any time during the validity of the refresh token, you can [refresh your access token](https://docs.developer.yelp.com/reference/refresh-access-token). The new access token will be valid for 7 days from the time of issue.

For [get access token v2](https://docs.developer.yelp.com/reference/oauth2_token), no new refresh token is issued for a new authorization request if there's already an existing active refresh token. Instead, that refresh token will be returned and the original refresh token expiry won't be changed.

[get access token v3](https://docs.developer.yelp.com/reference/oauth2_token_v3), in contrast, issues a new refresh token with a successful new authorization request.

## 

Step 1 - Getting an access and refresh token

Follow the [Authorization Code Workflow](https://docs.developer.yelp.com/docs/authorization-code-workflow) to get an access and refresh token.

## 

Step 2 - Refreshing an access token

There are two endpoints available to exchange a refresh token for a new access token:

- [get access token v2](https://docs.developer.yelp.com/reference/oauth2_token)
- [get access token v3](https://docs.developer.yelp.com/reference/oauth2_token_v3)

For either, call the endpoint using your refresh token from step 1. The endpoint will return a new access token. [get access token v3](https://docs.developer.yelp.com/reference/oauth2_token_v3) differs from v2 in the following ways:

1. In addition to the new access token, it will return a new refresh token for future use.
2. If an expired or otherwise invalid refresh token is used, the currently active refresh token is revoked.

### 

Reference documentation

Use `grant_type=refresh_token`

[![Get Access Token v2](https://files.readme.io/08035d8-small-yelp-dev-portal.png)\\ \\ ![docs.developer.yelp.com](https://files.readme.io/92f5032-small-174882.png)docs.developer.yelp.com\\ \\ Get Access Token v2](https://docs.developer.yelp.com/reference/oauth2_token)

### 

Sample Requests

#### 

get access token v2

HTTP

`POST /oauth2/token HTTP/1.1 Host: api.yelp.com Content-Type: application/x-www-form-urlencoded  client_id={client_id}& client_secret={client_secret}& grant_type=refresh_token& refresh_token={refresh_token_code}`

The authorization server responds with a new access token with HTTP status code 200 if the token has been refreshed successfully:

JSON

`{   "access_token": "<128_character_long_string>",   "token_type": "Bearer",   "expires_in": 10000,   "expires_on": "2016-08-26T15:25:16+00:00", }`

#### 

get access token v3

HTTP

`POST /oauth2/token/v3 HTTP/1.1 Host: api.yelp.com Content-Type: application/x-www-form-urlencoded  client_id={client_id}& client_secret={client_secret}& grant_type=refresh_token& refresh_token={refresh_token_code}`

The authorization server responds with a new access token and refresh token with HTTP status code 200 if the token has been refreshed successfully:

JSON

`{   "access_token": "<128_character_long_string>",   "token_type": "Bearer",   "expires_in": 10000,   "expires_on": "2016-08-26T15:25:16+00:00",   "refresh_token": "<128_character_long_string>",   "refresh_token_expires_in": 31535999,   "refresh_token_expires_on": "2025-10-11T23:23:10+00:00" }`

Updated over 1 year ago

---

Did this page help you?

Yes

No

Copy Page