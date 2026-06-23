# Source: https://docs.developer.yelp.com/reference/mark-lead-event-as-read

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

The request body of the POST /v3/leads/{lead\_id}/events/mark\_as\_read endpoint

event\_id

string

required

The encrypted id of the event which is being marked as read

time\_read

date-time

An optional parameter to specify the time when the event was read. If not provided, the event is considered read at the current timestamp (Refer [RFC3339](https://www.rfc-editor.org/rfc/rfc3339#section-5.6) for the format)

# 

201

All lead events before and including the specified event id were successfully marked as read

# 

400

This error is returned in any of the following scenarios:

- The provided lead ID in the URL is not recognized as a valid Yelp Lead ID.
- The provided event ID in the request body is not recognized as a valid Yelp Event ID.
- The event\_id parameter is missing from the request body.
- The time\_read parameter in the request body has an invalid value.

| code | description |
| --- | --- |
| INVALID\_ID | "The ID provided is not valid" |
| VALIDATION\_ERROR | "'event\_id' is a required property" |
| VALIDATION\_ERROR | "'Invalid-time-read-value' is not a 'date-time'" |

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

This error is returned in any of the following scenarios:

- The Lead with the given ID was not found
- The specified event ID does not exist
- The event ID which is being marked as read doesn't belong to the provided lead

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

201 - Success400 - Invalid Lead ID400 - Invalid Request Body401 - Unauthorized401 - Invalid Token403 - Business must be Advertising404 - Not Found429 - Rate limited500 - Internal Server Error

Updated about 1 year ago

---