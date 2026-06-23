# Source: https://docs.developer.yelp.com/reference/get-lead-ids-for-business

⚠️

This reference guide is currently experiencing difficulties and will be back online shortly. Please contact [support@readme.io](mailto:support@readme.io?subject=API Explorer Error [ERR-YR5GEB]) with your error code.

`ERR-YR5GEB`

business\_id

string

required

The Yelp Business ID

limit

integer

1 to 20

Defaults to 20

The maximum number of items to return. Default=20 (1-20).

after\_lead\_id

string

If specified, only lead IDs that come after this lead ID will be returned.

# 

200

The lead IDs were fetched successfully.

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

 \--url 'https://api.yelp.com/v3/businesses/business\_id/lead\_ids?limit=20' \\

3

 \--header 'accept: application/json'

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

200400 - Invalid Lead ID401 - Unauthorized401 - Invalid Token403 - Business must be Advertising404 - Not Found429 - Rate limited500 - Internal Server Error

Updated about 1 year ago

---

Did this page help you?

Yes

No