# Source: https://docs.developer.yelp.com/reference/get-lead-events

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

#### URL Expired

The URL for this request expired after 30 days.

> ## 📘
> 
> This endpoint is part of the Leads API, visit [Leads API](https://docs.developer.yelp.com/docs/leads-api) to learn more.

ID

string

required

The Yelp Lead ID

older\_than\_cursor

string

If specified, only events that were sent before this cursor will be returned.

newer\_than\_cursor

string

If specified, only events that were sent after this cursor will be returned.

limit

integer

1 to 20

Defaults to 20

The maximum number of items to return. Default: 20 (1-20). _Note_ Events with the same id (text + attachment) are counted as 1 event for the limit.

# 

200

List of lead events.

# 

400

The provided ID is not recognized as a valid Yelp Lead ID

# 

401

The API key has either expired or doesn't have the required scopes to query this endpoint.

| code | description |
| --- | --- |
| UNAUTHORIZED\_API\_KEY | The API key provided is not currently able to query this endpoint. |
| TOKEN\_INVALID | Invalid API key or authorization header. |

# 

403

This error is returned in any of the following scenarios:

- The business isn't currently advertising.
- The business user doesn't have access to the business.

| code | description |
| --- | --- |
| UNAUTHORIZED\_BUSINESS\_MINIMUM\_ADVERTISING | "You're not authorized to access this business as it does not meet minimum advertising requirements." |
| NO\_BUSINESS\_ACCESS | "You don't have access to this Business." |

# 

404

The Lead with the given ID was not found.

# 

429

You have either exceeded your daily quota, or have exceeded the queries-per-second limit for this endpoint. Try reducing the rate at which you make queries.

# 

500

Internal Server Error

Updated about 1 year ago

---

Did this page help you?

Yes

No

ShellNodeRubyPHPPython

Bearer

xxxxxxxxxx

1

curl \--request GET \\

2

 \--url 'https://api.yelp.com/v3/leads/ID/events?limit=20' \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200 - Events400 - Invalid Lead ID401 - Unauthorized401 - Invalid Token403 - Business must be Advertising404 - Not Found429 - Rate limited500 - Internal Server Error

Updated about 1 year ago

---

Did this page help you?

Yes

No