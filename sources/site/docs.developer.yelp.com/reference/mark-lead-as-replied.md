# Source: https://docs.developer.yelp.com/reference/mark-lead-as-replied

| Time | Status | User Agent | |
| :-- | :-- | :-- | :-- |
| 
Retrieving recent requests…

 |

Loading…

> ## 📘
> 
> This endpoint is part of the Leads API, visit [Leads API](https://docs.developer.yelp.com/docs/leads-api) to learn more.

ID

string

required

The Yelp Lead ID

Request body for creating an event.

The request object of the POST /v3/leads/{lead\_id}/mark\_as\_replied endpoint

reply\_type

string

enum

required

The medium through which the lead was replied to.

PHONEEMAIL

Allowed:

`PHONE``EMAIL`

# 

201

The lead was successfully marked as replied

# 

400

This error is returned in any of the following scenarios:

- The provided ID in the URL is not recognized as a valid Yelp Lead ID.
- The reply\_type parameter is missing from the request body.
- The reply\_type parameter has an invalid value.

| code | description |
| --- | --- |
| INVALID\_ID | "The ID provided is not valid" |
| VALIDATION\_ERROR | "'reply\_type' is a required property" |
| VALIDATION\_ERROR | "'InvalidValue' is not one of \['PHONE', 'EMAIL'\]" |

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

- The business user has been blocked from marking a lead as replied
- The business user has already marked a lead as replied
- The business isn't currently advertising.
- The business user doesn't have access to the business.

| code | description |
| --- | --- |
| NOT\_AUTHORIZED | "The user has been blocked" |
| NOT\_AUTHORIZED | "Lead already marked as replied" |
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

ShellNodeRubyPHPPython

Bearer

Loading…

Click `Try It!` to start a request and see the response here! Or choose an example:

application/json

201 - Success400 - Invalid Lead ID400 - Invalid Request Body401 - Unauthorized401 - Invalid Token403 - Business User Blocked403 - Business must be Advertising404 - Not Found429 - Rate limited500 - Internal Server Error

Updated about 1 year ago

---